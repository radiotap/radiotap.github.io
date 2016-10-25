XChannel
========

Bit Number 18

Structure u32 flags, u16 freq, u8 channel, u8 maxpower

Required Alignment 4

Unit(s) none, MHz, 802.11 channel number, unknown

Extended channel information. The `flags` part of the field contains
various flags:

\[Table not converted\]

Discussion
==========

This field is parsed by wireshark, but only partially (it ignores
maxpower). Origin of the field is unknown. Used by FreeBSD and OS X.

Channel numbers are problematic -- using the channel's center frequency
would be much better.

The flags define some things that can be inferred (2 vs. 5 GHz).

Things like the "Channel Type Passive" don't make sense per packet. As
used, this field conflates channel properties (which need not be stored
per packet but are more or less fixed) with packet properties (like the
modulation).
