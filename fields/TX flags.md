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

\[Table not converted\]

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
