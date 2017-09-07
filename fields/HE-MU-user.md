---
title: HE-MU-user
categories: [suggested]
---
Bit Number
: not assigned yet

Structure
: u16 per_user_1, per_user_2
  u8 per_user_position, per_user_known

Required Alignment
: 2

Unit(s)
: none

This field contains data from a SIG-B per-user field for those extra
users for which the data wasn't capture. This field isn't normally
necessary, if an HE_MU PPDU was captured, then typically only one of
the many users will be captured; in this case, adding this field one
or multiple times allows capturing the full contents of the SIG-B.

Note that the MCS/DCM/etc. configuration for the captured data is
already encoded in the regular [HE](HE) field, and for the SIG-B it's
part of the [HE-MU](HE-MU) field.

The split into parts 1 and 2 allows packing this more densely due to
then requiring alignment of only two.

## per_user_1

| **`0x7fff`** | B0-B14 of the HE-SIG-B user field as in spec |
| **`0x8000`** | (reserved) |

## per_user_2
| **`0x003f`** | B15-B20 of the HE-SIG-B user field as in spec |
| **`0xffc0`** | (reserved) |

## per_user_position

This contains the position of this user field, starting from 0.

## per_user_known

| **`0x01`** | user field position known |
| **`0x02`** | STA-ID known (B0-10) |
| **`0x04`** | NSTS known (B11-13, only for non-MU-MIMO) |
| **`0x08`** | Tx Beamforming known (B14, only for non-MU-MIMO) |
| **`0x10`** | Spatial Configuration known (B11-B14, only for MU-MIMO) |
| **`0x20`** | MCS known (B15-18) |
| **`0x40`** | DCM known (B19) |
| **`0x80`** | Coding known (B20) |
