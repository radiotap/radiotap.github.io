---
title: MCS
categories: [defined]
---
Bit Number
: 19

Structure
: u8 known, u8 flags, u8 mcs

Required Alignment
: 1

The `mcs` field indicates the MCS rate index as in
[IEEE\_802.11n-2009](http://en.wikipedia.org/wiki/IEEE_802.11n-2009#Data_rates)

The `known` field indicates which information is known:

|**flag**|**definition**|
| 0x01 | bandwidth |
| 0x02 | MCS index known (in mcs part of the field) |
| 0x04 | guard interval |
| 0x08 | HT format |
| 0x10 | FEC type |
| 0x20 | STBC known |
| 0x40 | Ness known (Number of extension spatial streams) |
| 0x80 | Ness data - bit 1 (MSB) of Number of extension spatial streams |

The `flags` field is any combination of the following:

| **flag** | **definition** |
| 0x03 | bandwidth - 0: 20, 1: 40, 2: 20L, 3: 20U |
| 0x04 | guard interval - 0: long GI, 1: short GI |
| 0x08 | HT format - 0: mixed, 1: greenfield |
| 0x10 | FEC type - 0: BCC, 1: LDPC |
| 0x60 | Number of STBC streams |
| 0x80 | Ness - bit 0 (LSB) of Number of extension spatial streams |
