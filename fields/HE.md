---
title: HE
categories: [suggested]
---
Bit Number
: not assigned yet

Structure
  - u16 data1, data2, data3, data4, data5

Required Alignment
: 2

Unit(s)
: none

The presence of this field indicates that the frame was received or
transmitted using the HE PHY.

This field contains data mostly from the HE-SIG-A part that is common
to all HE transmissions, but some of the data might also be calculated
(e.g. when included in the transmission of an HE_TRIG type frame, some
parameters are not included in the HE-SIG-A but were determined by the
trigger frame).
However, for PPDUs of HE_MU format, it contains the data that applies
to the encoding of the PSDU, with more detailed information about the
MU transmission contained in the [HE-MU](HE-MU) field if known.

In the case of MU transmissions, the [HE-MU-user](HE-MU-user) field may
also be present one or more times in that case to capture extra users
for which the data couldn't be captured; if the data was captured for
more than one user then multiple packets must be written into the
radiotap capture.

## data1

| **`0x0003`** | HE PPDU Format: 0=HE_SU, 1=HE_EXT_SU, 2=HE_MU, 3=HE_TRIG |
| **`0x0004`** | BSS Color known |
| **`0x0008`** | Beam Change known |
| **`0x0010`** | UL/DL known |
| **`0x0020`** | data MCS known |
| **`0x0040`** | data DCM known |
| **`0x0080`** | LDPC known |
| **`0x0100`** | LDPC extra symbol segment known |
| **`0x0200`** | STBC known |
| **`0x0400`** | Spatial Reuse known |
| **`0x0800`** | Spatial Reuse 2 known |
| **`0x1000`** | Spatial Reuse 3 known |
| **`0x2000`** | Spatial Reuse 4 known |
| **`0x4000`** | BW/RU allocation known |
| **`0x8000`** | Doppler known |

## data2

| **`0x0001`** | BW/RU allocation known |
| **`0x0002`** | GI known |
| **`0x0004`** | LTF known |
| **`0x0008`** | Pre-FEC Padding Factor known |
| **`0x0010`** | TxBF known |
| **`0x0020`** | PE Disambiguity known |
| **`0x0040`** | TXOP known |
| **`0x0080`** | Doppler value |
| **`0x7f00`** | TXOP value |
| **`0x8000`** | (reserved) |

## data3

| **`0x003f`** | BSS Color |
| **`0x0040`** | Beam Change |
| **`0x0080`** | UL/DL |
| **`0x0f00`** | data MCS (not SIG-B MCS from HE-SIG-A for HE_MU format) |
| **`0x1000`** | data DCM (cf. data MCS) |
| **`0x2000`** | LDPC |
| **`0x4000`** | LDPC extra symbol segment |
| **`0x8000`** | STBC |

## data4

| **`0x000f`** | Spatial Reuse |
| **`0x00f0`** | Spatial Reuse 2 (HE_TB format PPDU only) |
| **`0x0f00`** | Spatial Reuse 3 (HE_TB format PPDU only) |
| **`0xf000`** | Spatial Reuse 4 (HE_TB format PPDU only) |

## data5

| **`0x000f`** | data Bandwidth/RU allocation (0=20, 1=40, 2=80, 3=160/80+80, 4=26-tone RU, 5=52-tone RU, 6=106-tone RU, 7=242-tone RU, 8=484-tone RU, 9=996-tone RU, 10=2x996-tone RU |
| **`0x0030`** | GI (0=0.8us, 1=1.6us, 2=3.2us, 3=reserved) |
| **`0x00c0`** | LTF (0=1x, 1=2x, 2=4x, 3=reserved) |
| **`0x0f00`** | NSTS (actual number of space-time streams, 0=unknown, 1=1, etc.) |
| **`0x3000`** | Pre-FEC Padding Factor |
| **`0x4000`** | TxBF |
| **`0x8000`** | PE Disambiguity |
