---
title: HE-MU
categories: [suggested]
---
Bit Number
: 24 (tentatively assigned, field data may change)

Structure
: - u16 flags1
  - u16 flags2
  - u8 RU[4]

Required Alignment
: 2

Unit(s)
: none

This field contains data related to PPDUs of HE_MU type that wasn't
already captured in the regular [HE](HE) field. This is the common
data (from HE-SIG-A and HE-SIG-B), the per-user data can be captured
in the [HE-MU-other-user](HE-MU-other-user) field.

## flags1

| **`0x000f`** | SIG-B MCS (from SIG-A) |
| **`0x0010`** | SIG-B MCS known |
| **`0x0020`** | SIG-B DCM (from SIG-A) |
| **`0x0040`** | SIG-B DCM known |
| **`0x0080`** | Bandwidth from SIG-A known |
| **`0x0100`** | RU[0] known (presence depends on bandwidth) |
| **`0x0200`** | RU[1] known (presence depends on bandwidth) |
| **`0x0400`** | RU[2] known (presence depends on bandwidth) |
| **`0x0800`** | RU[3] known (presence depends on bandwidth) |
| **`0x1000`** | Center 26-tone RU bit known |
| **`0x2000`** | Center 26-tone RU value |
| **`0x4000`** | SIG-B Compression known |
| **`0x8000`** | SIG-B Symbols/MU-MIMO Users known |

## flags2

| **`0x0007`** | Bandwidth from SIG-A |
| **`0x0008`** | SIG-B compression from SIG-A |
| **`0x00f0`** | # of HE-SIG-B Symbols - 1 or # of MU-MIMO Users - 1 from SIG-A |
| **`0x0100`** | (reserved) |
| **`0x0200`** | # of HE-SIG-B Symbols/MU-MIMO users known |
| **`0x0c00`** | (reserved) |
| **`0x7000`** | # of HE-LTF Symbols from SIG-A |
| **`0x8000`** | # of HE-LTF Symbols known |

## RU

Each of these contains the 8 bit RU assignment index, if indicated as
present in the flags.
