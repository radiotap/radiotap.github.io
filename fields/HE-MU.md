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

## Channel 1 / Channel 2 usage and RU byte mapping

The "Channel 1" and "Channel 2" specific fields (respectively "channel1
and channel2" on the RU fields) are used in the following way:

 * Channel 1's known field is always used, use it to indicate how much
   data of channel 1 was captured
 * Channel 2's known field is only used for 40 MHz and higher, use it to
   indicate how much data of channel 2 was captured, it should be set to
   0 (for unknown) for 20 MHz

The following tables map the RU fields to tone ranges:

### Channel 1 tones depending on known field

If known=0, no data was reported (e.g. HW not capable, or CRC error on one of the SIG-Bs).

| **RU idx** | **known=1 (20 MHz)** | **known=2 (40 MHz)** | **known=3 (80 MHz)** | **known=4 (160 MHz)** |
| **RU[0]** | -122:122 | -244:-3 | -500:-259 | -1012:-771 |
| **RU[1]** | / | / | 17:258 | -495:-254 |
| **RU[2]** | / | / | / | 12:253 |
| **RU[3]** | / | / | / | 529:770 |
| **Center 26-tone** | / | / | -16:-4, 4:16 | -528:-516, -508:-496 |

### Channel 2 tones depending on known field

If known=0, no data was reported (e.g. HW not capable, or CRC error on one of the SIG-Bs).

| **RU idx** | **known=1 (20 MHz)** | **known=2 (40 MHz)** | **known=3 (80 MHz)** | **known=4 (160 MHz)** |
| **RU[0]** | / | 3:244 | -258:-17 | -770:529 |
| **RU[1]** | / | / | 259:500 | -253:-12 |
| **RU[2]** | / | / | / | 254:495 |
| **RU[3]** | / | / | / | 771:1012 |
| **Center 26-tone** | / | / | / | 496:508, 516:528 |

## flags1

| **`0x000f`** | SIG-B MCS (from SIG-A) |
| **`0x0010`** | SIG-B MCS known |
| **`0x0020`** | SIG-B DCM (from SIG-A) |
| **`0x0040`** | SIG-B DCM known |
| **`0x0080`** | (Channel 2) Center 26-tone RU bit known |
| **`0x0700`** | Channel 1 RU known |
| **`0x0800`** | (reserved) |
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
| **`0x7000`** | Channel 2 RU known |
| **`0x8000`** | (reserved) |

## RU

Each of these contains the 8 bit RU assignment index, if indicated as
present in the flags.
