---
title: Introduction
---
Radiotap is a [de facto](http://en.wikipedia.org/wiki/De_facto) standard
for 802.11 frame injection and reception. This page intends to document
its progress and development and serve as a forum for developers helping
to advance this standard.

Discussion
----------

-   Takes place on the radiotap mailing list, to subscribe mail

        subscribe radiotap

    to `majordomo -AT- radiotap.org`

-   Archive at gmane:
    <http://news.gmane.org/gmane.network.wireless.radiotap>
-   [Discussion summaries on this wiki](../Discussion)
-   After discussing, start the [standardisation
    process](../Standardisation).

Operating System support
------------------------

The following Operating Systems support radiotap. A link is provided to
their implementation support page.

-   [FreeBSD](http://www.freebsd.org/cgi/man.cgi?query=ieee80211_radiotap)
-   [Linux](http://linuxwireless.org/en/developers/Documentation/radiotap)
-   [NetBSD](http://netbsd.gw.com/cgi-bin/man-cgi?ieee80211_radiotap+9+NetBSD-current)
-   [OpenBSD](http://www.openbsd.org/cgi-bin/man.cgi?query=ieee80211_radiotap)
-   Windows (with
    [AirPcap](https://www.cacetech.com/products/airpcap.html))

Parser libraries
----------------

There are a number of ad-hoc parsers contained in various programs, but
there's at least one parser library as well, which evolved from the code
used in Linux:

-   <https://github.com/radiotap/radiotap-library>

Background
----------

The radiotap header format is a mechanism to supply additional
information about frames, from the driver to userspace applications such
as libpcap, and from a userspace application to the driver for
transmission. Designed initially for NetBSD systems by David Young, the
radiotap header format provides more flexibility than the Prism or AVS
header formats and allows the driver developer to specify an arbitrary
number of fields based on a bitmask presence field in the radiotap
header.

Why we need it
--------------

The radiotap header provides more flexibility for reporting the
characteristics of frames than the legacy Prism or AVS headers allow.
For example, it is not currently possible to report the Frame Check
Sequence (FCS) information in the Prism header; adding the FCS
information to the header would break other parsers that expect the
Prism header to be a consistent 144 bytes in length. Radiotap is
flexible enough to accommodate the addition of new fields over time,
without breaking existing parsers.

Detail
------

The radiotap capture format starts with a radiotap header:

    struct ieee80211_radiotap_header {
            u_int8_t        it_version;     /* set to 0 */
            u_int8_t        it_pad;
            u_int16_t       it_len;         /* entire length */
            u_int32_t       it_present;     /* fields present */
    } __attribute__((__packed__));

The *it\_version* field indicates which major version of the radiotap
header is in use. Currently, this is always 0. Adding support for
additional radiotap fields does not change the version number.

The *it\_pad* field is currently unused, it simply aligns the fields
onto natural word boundaries.

The *it\_len* field indicates the entire length of the radiotap data,
including the radiotap header. This is valuable for the developer so
they can consistently locate the beginning of the 802.11 frame that
follows the radiotap data, even if their parser doesn't understand all
of the data fields specified.

The *it\_present* field is a bitmask of the radiotap data fields that
follows the radiotap header.

Provided bit 31 of the `it_present` field is not set, the data for
fields specified in the `it_present` bitmask immediately follow the
radiotap header. If it is set, then more `it_present` words follow and
the radiotap data follows after the `it_present` word that has bit 31
unset. Multiple namespaces may be present.

One of the advantages of radiotap is that new fields can be added to the
end of the radiotap data without breaking existing parsers. If a parser
identifies a bitmask value that is not recognized, it can skip to the
end of the radiotap data by referencing the header `it_len` field.

### Important Radiotap Characteristics

-   Fields are strictly ordered; The developer can specify any
    combination of fields, but the data must appear following the
    radiotap header in the order they are specified in the `it_present`
    bitmask (or more accurately, in the order the bit numbers for the
    `it_present` bitmask are defined).
-   Data is specified in little endian byte-order, all data fields
    including the `it_version`, `it_len` and `it_present` fields in the
    radiotap header are to be specified in little endian byte-order.
-   Field lengths are implicit: the radiotap header format does not
    specify field lengths, it is expected that the developer knows the
    corresponding length based on the data field name.
-   Variable-length fields are not supported since field lengths
    are implicit.
-   Support for extended bitmasks, see below.
-   Natural alignment field requirement; Radiotap requires that all
    fields be *naturally aligned*. See the section **Alignment in
    Radiotap** below for more information.

Extended presence masks
-----------------------

If bit 31 of the `it_present` field is set, an extended `it_present`
bitmask is present. Radiotap parsers must check for the presence of bit
31 in the `it_present` field to identify if a second 32-bit bitmask
follows the radiotap header before the radiotap data. Additional
bitmasks may be chained to the end of extended bitmasks by setting bit
31 in each bitmask to indicate a follow-up one. Field bits in an
extended bitmask still counted starting from 32, 64, etc. so that field
number 63 is also reserved because bit 31 is reserved in every
(extended) bitmask.

For example, these bytes, written in binary/hex (words are in little
endian so this is a byte-wise representation of a radiotap header):

    00000000 00000000 nnnnnnnn nnnnnnnn  |  00 00 nn nn
    00000010 00000000 00000000 10000000  |  02 00 00 80
    00000110 00000000 00000000 10000000  |  06 00 00 80
    00000011 00000000 00000000 00000000  |  03 00 00 00

    (radiotap data follows)

define a valid radiotap header that has fields 1, 33, 34, 64 and 65. The
nnn indicates that the length needs to be filled in there.

Radiotap fields
---------------

Defined (and suggested) fields are listed with their bit number. Due to
the use of bit 31 to indicate a chained bitmask, the values 31, 63, etc.
(`n * 32 - 1`) are reserved. Vendor-specified namespaces and radiotap
namespace reset additionally reserves bits 29 and 30 in each bitmask as
well, extending the reserved numbers to 29, 30, 31, 61, 62, 63, etc.
(`n * 32 - 3`, `n * 32 - 2`, `n * 32 - 1`).

-   [defined fields](/fields/defined)
-   [suggested fields](/fields/suggested)
-   [rejected fields](/fields/rejected)

Alignment in Radiotap
---------------------

Radiotap requires that all fields in the radiotap header are aligned to
natural boundaries. For radiotap, that means all 8-, 16-, 32-, and
64-bit fields must begin on 8-, 16-, 32-, and 64-bit boundaries,
respectively. In this way, generators and parsers can avoid unaligned
accesses to radiotap capture fields. Radiotap-compliant generators must
insert padding before a capture field to ensure its natural alignment.
Radiotap-compliant packet parsers, such as tcpdump(8), expect and skip
the padding.

Note: structs are not packed identically on all architectures and
compilers. If a radiotap header is created with a packed structure it is
important to insert padding bytes manually in order to ensure natural
alignment.

For example, if a developer wants to construct a radiotap header as
follows:

    struct rtapdata {
        uint8_t  antsignal;
        uint16_t tx_attenuation;
        uint8_t  flags;
        uint16_t rx_flags;
    } __attribute__ ((packed));

This would cause the fields `tx_attenuation` and `rx_flags` to be
potentially *unnaturally aligned*. Because the radiotap data fields are
in a strict order with a fixed length, it is not always possible to get
the alignment to fall on an natural boundary using only the radiotap
data fields. Therefore, it is sometimes necessary to pad these fields.
In this example, you would insert padding like this:

    struct rtapdata {
        uint8_t  antsignal;
        uint8_t  pad_for_tx_attentuation; // <-- added
        uint16_t tx_attenuation;
        uint8_t  flags;
        uint8_t  pad_for_rx_flags;        // <-- added
        uint16_t rx_flags;
    } __attribute__ ((packed));

One thing that can be confusing is the fact that there is some radiotap
data that consists of multiple fields. For example the [Channel
field](/fields/Channel) consists of two 16-bit quantities and
both of them require 16-bit alignment, although the Channel data
consists of 32 bits in total.
