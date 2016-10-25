---
title: XChannel
categories: [suggested]
---
Bit Number
: 18

Structure
: u32 flags, u16 freq, u8 channel, u8 maxpower

Required Alignment
: 4

Unit(s) none, MHz, 802.11 channel number, unknown

Extended channel information. The `flags` part of the field contains
various flags:

| **flag** | **definition** |
| `0x00000010` | Channel Type Turbo |
| `0x00000020` | Channel Type Complementary Code Keying (CCK) Modulation |
| `0x00000040` | Channel Type Orthogonal Frequency-Division Multiplexing (OFDM) |
| `0x00000080` | Channel Type 2 GHz spectrum |
| `0x00000100` | Channel Type 5 GHz spectrum |
| `0x00000200` | Channel Type Passive |
| `0x00000400` | Channel Type Dynamic CCK-OFDM Channel |
| `0x00000800` | Channel Type Gaussian Frequency Shift Keying (GFSK) Modulation |
| `0x00001000` | Channel Type GSM |
| `0x00002000` | Channel Type Status Turbo |
| `0x00004000` | Channel Type Half Rate |
| `0x00008000` | Channel Type Quarter Rate |
| `0x00010000` | Channel Type HT/20 |
| `0x00020000` | Channel Type HT/40+ |
| `0x00040000` | Channel Type HT/40- |

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
