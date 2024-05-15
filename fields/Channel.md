---
title: Channel
categories: [defined]
type: 3
---
Bit Number
: 3

Structure
: u16 frequency, u16 flags

Required Alignment
: 2

Units
: MHz, bitmap

Tx/Rx frequency in MHz, followed by flags.

Currently, the following flags are defined:


| **Mask** | **Meaning** |
| 0x0010 | Turbo Channel |
| 0x0020 | CCK channel |
| 0x0040 | OFDM channel |
| 0x0080 | 2 GHz spectrum channel |
| 0x0100 | 5 GHz spectrum channel |
| 0x0200 | Only passive scan allowed |
| 0x0400 | Dynamic CCK-OFDM channel |
| 0x0800 | GFSK channel (FHSS PHY) |
