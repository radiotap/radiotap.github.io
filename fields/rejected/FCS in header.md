FCS in header
=============

Bit Number 14 (clashes with official assignment of bit 14)

Structure u32 FCS

Required Alignment 4

Field containing the FCS of the frame (instead of it being appended to
the frame as it would appear on the air.)

Discussion
==========

This field originates from OpenBSD. It is parsed by wireshark, but
clashes with defined-fields/RX flags\_.

This field should not be added since FCS-at-end is more natural.
