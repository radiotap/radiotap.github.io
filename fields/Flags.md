---
title: Flags
categories: [defined]
---
Bit Number
: 1

Structure
: u8 flags

Unit
: bitmap

Properties of transmitted and received frames.

Currently, the following flags are defined:

| **Mask** | **Meaning** |
| 0x01 | sent/received during CFP |
| 0x02 | sent/received with short preamble |
| 0x04 | sent/received with WEP encryption |
| 0x08 | sent/received with fragmentation |
| 0x10 | frame includes FCS |
| 0x20 | frame has padding between 802.11 header and payload (to 32-bit boundary) |
| 0x40 | frame failed FCS check |

Currently unspecified but used:

| **Mask** | **Meaning** |
| 0x80 | frame used short guard interval (HT) |
