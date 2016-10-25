---
title: RX flags
categories: [defined]
---
Bit Number
: 14

Structure
: u16

Required Alignment
: 2

Unit
: bitmap

Properties of received frames.

The following flags are currently defined:

| **mask** | **meaning** |
| `0x0001` | reserved (was FCS failed but this is a regular flag) |
| `0x0002` | PLCP CRC check failed |
| `0xfffc` | reserved for future expansion |

Notes
=====

This field originates from NetBSD and is also used like this in Linux.

Use bit `0x40` in the [flags field](/fields/Flags) to indicate *FCS CRC
failed*.
