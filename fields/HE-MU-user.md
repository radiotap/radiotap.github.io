---
title: HE-MU-user
categories: [suggested]
---
Bit Number
: not assigned yet

Structure
: u32 sig_B_user
  u32 sig_B_user_known

Required Alignment
: 4

Unit(s)
: none

This field contains data from the SIG-B per-user field. One such field
shall be used for each user field for which data is known.


## sig_B_user

| **`0x001fffff`** | HE-SIG-B user field as in spec |
| **`0x7fe00000`** | (reserved) |
| **`0x80000000`** | MU-MIMO allocation (1: MU-MIMO, 0: non-MU-MIMO) |

## sig_B_user_known

| **`0x000000ff`** | user field position (starting from 0) |
| **`0x00000100`** | user field position known |
| **`0x00000200`** | the captured MPDU is for this user |
| **`0x00000c00`** | (reserved) |
| **`0x0000f000`** | bandwidth (see below) |
| **`0x00010000`** | bandwidth known |
| **`0x00020000`** | STA-ID known (B0-10) |
| **`0x00040000`** | NSTS known (B11-13, only for non-MU-MIMO) |
| **`0x00080000`** | Tx Beamforming known (B14, only for non-MU-MIMO) |
| **`0x00100000`** | Spatial Configuration known (B11-B14, only for MU-MIMO) |
| **`0x00200000`** | MCS known (B15-18) |
| **`0x00400000`** | DCM known (B19) |
| **`0x00800000`** | Coding known (B20) |
| **`0xff000000`** | (reserved) |

Of course only a single field shall indicate that the captured MPDU was
recorded for this user, if multiple users were recorded the bits shall be
varied accordingly.

### bandwidth values

| 0 | 2 MHz |
| 1 | 5 MHz |
| 2 | 10 MHz |
| 3 | 20 MHz |
| 4 | 40 MHz |
| 5 | 80 MHz |
| 6 | 160 MHz |
| 7 | (reserved) |

This field isn't present in the spec, it's normally implied by the RU
allocations, but not all of those are always recorded in the radiotap header
so this field is necessary. Note that implementations should include this
field even when the RU allocation etc. are all known, to simplify parsing.
Without this field, the effective bitrate is otherwise unknown.
