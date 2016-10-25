Vendor Namespace
================

Bit Number not applicable, bit 30 in *every* `it_present` word

Structure u8 OUI\[3\], u8 sub\_namespace, u16 skip\_length

Required Alignment 2

This field is reserved in **all namespaces and every** `it_present`
**word**, the standard radiotap namespace as well as all vendor
namespaces. It is mutually exclusive with the *Reset to Radiotap
Namespace* field, setting both is undefined.

The Vendor Namespace Field contains three sub-fields. The first
sub-field is 3 bytes long. It contains the vendor's IEEE 802
Organizationally Unique Identifier (OUI). The fourth byte is a
vendor-specific "namespace selector."

Before it resumes interpretation of presence bits in the following
32-bit presence words, if any, the interpreter shall reset its
presence-bitmap index to 0, and change to the vendor namespace specified
by the OUI and selector.

The fifth and sixth bytes, `skip_length`, comprise a 16 bit
little-endian value that tells the interpreter how many bytes of data
after the end of the Vendor Namespace Field can only be interpreted
according to the vendor namespace. If a radiotap header changes to a
namespace that the interpreter does not understand, and back, the
interpreter may resume interpretation in the new namespace by skipping
skip\_length data bytes after the end of the Vendor Namespace Field. If
a radiotap header changes from a vendor namespace to another vendor
namespace, the 6-byte data describing the new vendor namespace shall not
be accounted for in `skip_length`.
