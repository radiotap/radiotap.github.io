---
title: 0-length-PSDU
categories: [suggested]
---
Bit Number
: 26

Structure
  - u8 type

Required Alignment
: None

Unit(s)
: none

The presence of this field indicates that there was no PSDU in or
captured for this PPDU, only the PHY data is valid and the radiotap
header is not followed by an 802.11 header.

The type field indicates the type of PPDU.

| **type value** | **meaning** |
| 0              | sounding PPDU |
| 1              | data not captured (e.g. multi-user PPDU) |
| 0xff           | vendor-specific |
