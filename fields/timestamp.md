---
title: timestamp
categories: [defined]
---
Bit Number
: 22

Structure
: u64 timestamp, u16 accuracy, u8 unit/position, u8 flags

Required Alignment
: 8

Units
: as defined, as defined, none, none

timestamp
---------

The timestamp itself, in the unit defined in the field itself.

precision
---------

Defines the expected accuracy of the timestamp, in the same units as the
timestamp.

unit/position
-------------

| **flag** | **meaning** |
| `0x000F` | unit - see below |
| `0x00F0` | sampling position - see below |

### units

| **value** | **unit** |
| 0 | milliseconds |
| 1 | microseconds |
| 2 | nanoseconds |
| 3-15 | reserved |

### sampling positions

| **value** | **sampling position** |
| 0 | first bit (or symbol containing it) of MPDU - matches TSFT field |
| 1 | signal acquisition at start of PLCP |
| 2 | end of PPDU |
| 3 | end of MPDU (after FCS) |
| 4-14 | reserved |
| 15 | unknown or vendor/OOB defined |

flags
-----

| `0x01` | 32-bit counter (high 32 bits are unused) |
| `0x02` | accuracy known |
| `0xFC` | reserved |
