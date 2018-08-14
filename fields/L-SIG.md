---
title: L-SIG
categories: [suggested]
---
Bit Number
: 27

Structure
  - u16 data1, data2

Required Alignment
: 2

Unit(s)
: none

This field indicates - if known - the contents of the L-SIG.

## data1

| **`0x0001`** | rate known |
| **`0x0002`** | length known |
| **`0xfffc`** | (reserved) |

## data2

| **`0x000f`** | rate |
| **`0xfff0`** | length |
