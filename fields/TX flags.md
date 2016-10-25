---
title: TX flags
categories: [suggested]
---
Bit Number
: 15

Structure
: u16 flags

Required Alignment
: 2

Unit
: bitmap

Properties of transmitted frames.

|**mask** |**meaning** |
|`0x0001` |Transmission failed due to excessive retries |
|`0x0002` |Transmission used CTS-to-self protection |
|`0x0004` |Transmission used RTS/CTS handshake |
|`0x0008` |Transmission shall not expect an ACK frame and not retry when no ACK is received |
|`0x0010` |Transmission includes a pre-configured sequence number that should not be changed by the driver's TX handlers |

Discussion
==========

Used by NetBSD and Linux, clashes with ../hardware queue\_ as used in
OpenBSD.

The no-ack bit (0x0008) is used for uses of radiotap when frames are
sent. Similarly, the no-seq bit (0x0010) is used to allow userspace to
send frames with a specific sequence number (e.g. when transmitting
fragments of a single frame one-by-one). When it is set, the frame
should be transmitted with the sequence number included in the 802.11
MAC header of the frame as received from userspace, regardless of the
state of the sequence counters in driver/hardware.
