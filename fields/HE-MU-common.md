---
title: HE-MU-common
categories: [suggested]
---
Bit Number
: not assigned yet

Structure
: - u8 sig_B_common_RU[4]
  - u16 sig_B_common
  - u16 sig_B_common_known

Required Alignment
: 2

Unit(s)
: none

This field contains data from the HE-SIG-B field contained in HE_MU
frames.

## sig_B_common_RU

Each of these contains the 8 bit RU assignment index, if indicated as
present in the sig_B_common_known part.

## sig_B_common

| **`0x0001`** | Center 26-tone RU bit |
| **`0x07fe`** | CRC/Tail of SIG-B common |
| **`0xf800`** | reserved |

## sig_B_common_known

| **`0x0001`** | sig_B_common_RU[0] known (presence depends on SIG-A bandwidth) |
| **`0x0002`** | sig_B_common_RU[1] known (presence depends on SIG-A bandwidth) |
| **`0x0004`** | sig_B_common_RU[2] known (presence depends on SIG-A bandwidth) |
| **`0x0008`** | sig_B_common_RU[3] known (presence depends on SIG-A bandwidth) |
| **`0x0010`** | Center 26-tone RU bit is known (if it was present at all, which depends on SIG-A bandwidth) |
| **`0x0020`** | CRC field value is known |
| **`0x0040`** | Tail field value is known |
| **`0xFF80`** | (reserved) |
