---
title: S1G
categories: [suggested]
---
Type
: 32 

Structure
: u16 known, u16 data1, u16 data2

Required Alignment
: 2

Unit(s)
: none

The presence of this field indicates the frame was capture using an S1G phy.

## known

This field indicates the (known) contents of the S1G.

| **`0x0001`** | S1G PPDU Format Known |
| **`0x0002`** | Response Indication Known |
| **`0x0004`** | Guard Interval Known |
| **`0x0008`** | NSS Known | 
| **`0x0010`** | Bandwidth Known |
| **`0x0020`** | MCS Known |
| **`0x0040`** | Color Known |
| **`0x0080`** | Uplink Indication Known |
| **`0xFF00`** | Reserved |

## data1

| **`0x0003`** | S1G PPDU Format: 0=S1G_1M, 1=S1G_SHORT, 2=S1G_LONG |
| **`0x000C`** | Response Indication: 0=NO-RESPONSE, 1=NDP_RESPONSE, 2=NORMAL_RESPONSE, 3=LONG_RESPPNSE |
| **`0x0010`** | Reserved |
| **`0x0020`** | Guard Interval: 0=Long GI, 1=Short GI |
| **`0x00C0`** | Number Spatial Streams: 0=1 Spatial stream, 1=2, .. 3=4 Spatial streams |
| **`0x0F00`** | Bandwidth: 0=1MHz, 1=2MHz, 2=4MHz, 3=8MHz, 4=16MHz, 5-15 reserved |
| **`0xF000`** | MCS (MCS rate index, 0-10, 11-15 reserved) |

## data2

| **`0x0007`** | Color: 0-7 |
| **`0x0008`** | Uplink indication |
| **`0x00F0`** | Reserved |
| **`0xFF00`** | RSSI |
