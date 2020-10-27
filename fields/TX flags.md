---
title: TX flags
categories: [defined]
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
|`0x0020` |Transmission should not be reordered relative to other frames that have this flag set |

Discussion
==========

The no-ack bit (0x0008) is used for uses of radiotap when frames are
sent. Similarly, the no-seq bit (0x0010) is used to allow userspace to
send frames with a specific sequence number (e.g. when transmitting
fragments of a single frame one-by-one). When it is set, the frame
should be transmitted with the sequence number included in the 802.11
MAC header of the frame as received from userspace, regardless of the
state of the sequence counters in driver/hardware.

When the DONT_REORDER bit (0x0020) is set, injected frames aren't reordered
relative to other frames that also have this bit set (even when these
frames have different QoS TID values).
