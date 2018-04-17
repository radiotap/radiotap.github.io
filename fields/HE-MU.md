---
title: HE-MU
categories: [suggested]
---
Bit Number
: 24 (tentatively assigned, field data may change)

Structure
: - u16 flags1
  - u16 flags2
  - u8 RU_channel1[4]
  - u8 RU_channel2[4]

Required Alignment
: 2

Unit(s)
: none

This field contains data related to PPDUs of HE_MU type that wasn't
already captured in the regular [HE](HE) field. This is the common
data (from HE-SIG-A and HE-SIG-B), the per-user data can be captured
in the [HE-MU-other-user](HE-MU-other-user) field.

Note that the "Channel 1" and "Channel 2" specific fields (respectively
"channel1 and channel2" on the RU fields) are only both used for separate
SIG-B transmissions in 160 MHz PPDUs. Otherwise, "Channel 2" shall not be
used and "Channel 1" references the only SIG-B transmission. Cf. the
802.11ax amendment's Frequency Domain mapping description.

As a result, depending on bandwidth, the fields are only partially used:
 *  20 MHz: only Channel 1: RU[0]
 *  40 MHz: Only Channel 1: RU[0-1]
 *  80 MHz: Only Channel 1: RU[0-3], center 26-tone RU
 * 160 MHz: all fields

## flags1

| **`0x000f`** | SIG-B MCS (from SIG-A) |
| **`0x0010`** | SIG-B MCS known |
| **`0x0020`** | SIG-B DCM (from SIG-A) |
| **`0x0040`** | SIG-B DCM known |
| **`0x0080`** | (Channel 2) Center 26-tone RU bit known |
| **`0x0100`** | RU_channel1[0] known (presence depends on bandwidth) |
| **`0x0200`** | RU_channel1[1] known (presence depends on bandwidth) |
| **`0x0400`** | RU_channel1[2] known (presence depends on bandwidth) |
| **`0x0800`** | RU_channel1[3] known (presence depends on bandwidth) |
| **`0x1000`** | (Channel 1) Center 26-tone RU bit known |
| **`0x2000`** | (Channel 1) Center 26-tone RU value |
| **`0x4000`** | SIG-B Compression known |
| **`0x8000`** | # of HE-SIG-B Symbols/MU-MIMO Users known |

## flags2

| **`0x0003`** | bandwidth from Bandwidth field in HE-SIG-A (0 - 20 MHz, ..., 3 - 160/80+80 MHz) |
| **`0x0004`** | bandwidth from Bandwidth field in HE-SIG-A known |
| **`0x0008`** | SIG-B compression from SIG-A |
| **`0x00f0`** | # of HE-SIG-B Symbols - 1 or # of MU-MIMO Users - 1 from SIG-A |
| **`0x0300`** | preamble puncturing from Bandwidth field in HE-SIG-A (0 - non-puncturing, 1 - punctured secondary 20 MHz (in primary 80 MHz if applicable), 2 - punctured but primary 40 MHz is present (in primary 80 MHz if applicable) |
| **`0x0400`** | preamble puncturing from Bandwidth field in HE-SIG-A known |
| **`0x0800`** | (Channel 2) Center 26-tone RU value |
| **`0x1000`** | RU_channel2[0] known (presence depends on bandwidth) |
| **`0x2000`** | RU_channel2[1] known (presence depends on bandwidth) |
| **`0x4000`** | RU_channel2[2] known (presence depends on bandwidth) |
| **`0x8000`** | RU_channel2[3] known (presence depends on bandwidth) |

## RU

Each of these contains the 8 bit RU assignment index, if indicated as
present in the flags.
