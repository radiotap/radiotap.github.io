---
title: HE
categories: [suggested]
---
Bit Number
: 23 (tentatively assigned, field data may change)

Structure
  - u16 data1, data2, data3, data4, data5, data6

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
MU transmission contained in the [HE-MU](HE-MU) field if needed, in
many cases that field will not be needed as all the data about the
single user that was captured is already encoded here.

In the case of MU transmissions, the [HE-MU-other-user](HE-MU-other-user)
field may also be present one or more times in that case to capture extra
users for which the data couldn't be captured; if the data was captured
for more than one user then multiple packets must be written into the
radiotap capture.

## data1

| **`0x0003`** | HE PPDU Format: 0=HE_SU, 1=HE_EXT_SU, 2=HE_MU, 3=HE_TRIG |
| **`0x0004`** | BSS Color known |
| **`0x0008`** | Beam Change known |
| **`0x0010`** | UL/DL known |
| **`0x0020`** | data MCS known |
| **`0x0040`** | data DCM known |
| **`0x0080`** | Coding known |
| **`0x0100`** | LDPC extra symbol segment known |
| **`0x0200`** | STBC known |
| **`0x0400`** | Spatial Reuse known (Spatial Reuse 1 for HE_TRIG format) |
| **`0x0800`** | Spatial Reuse 2 known (HE_TRIG format), STA-ID known (HE_MU format) |
| **`0x1000`** | Spatial Reuse 3 known (HE_TRIG format) |
| **`0x2000`** | Spatial Reuse 4 known (HE_TRIG format) |
| **`0x4000`** | data BW/RU allocation known |
| **`0x8000`** | Doppler known |

## data2

| **`0x0001`** | pri/sec 80 MHz known |
| **`0x0002`** | GI known |
| **`0x0004`** | LTF symbols known |
| **`0x0008`** | Pre-FEC Padding Factor known |
| **`0x0010`** | TxBF known |
| **`0x0020`** | PE Disambiguity known |
| **`0x0040`** | TXOP known |
| **`0x0080`** | midamble periodicity known |
| **`0x3f00`** | RU allocation offset |
| **`0x4000`** | RU allocation offset known |
| **`0x8000`** | pri/sec 80 MHz (primary=0, secondary=1) |

## data3

| **`0x003f`** | BSS Color |
| **`0x0040`** | Beam Change |
| **`0x0080`** | UL/DL |
| **`0x0f00`** | data MCS (not SIG-B MCS from HE-SIG-A for HE_MU format) |
| **`0x1000`** | data DCM (cf. data MCS) |
| **`0x2000`** | Coding (0=BCC, 1=LDPC) |
| **`0x4000`** | LDPC extra symbol segment |
| **`0x8000`** | STBC |

## data4

| **bits** | **HE_SU and HE_EXT_SU format PPDU** |
| **`0x000f`** | Spatial Reuse |
| **`0xfff0`** | (reserved) |

| **bits** | **HE_TRIG format PPDU** |
| **`0x000f`** | Spatial Reuse 1 |
| **`0x00f0`** | Spatial Reuse 2 |
| **`0x0f00`** | Spatial Reuse 3 |
| **`0xf000`** | Spatial Reuse 4 |

| **bits** | **HE_MU format PPDU** |
| **`0x000f`** | Spatial Reuse |
| **`0x7ff0`** | STA-ID of the user for which the data was captured |
| **`0x8000`** | (reserved) |

## data5

| **`0x000f`** | data Bandwidth/RU allocation (0=20, 1=40, 2=80, 3=160/80+80, 4=26-tone RU, 5=52-tone RU, 6=106-tone RU, 7=242-tone RU, 8=484-tone RU, 9=996-tone RU, 10=2x996-tone RU) |
| **`0x0030`** | GI (0=0.8us, 1=1.6us, 2=3.2us, 3=reserved) |
| **`0x00c0`** | (reserved)
| **`0x0700`** | LTF symbols (0=1x, 1=2x, 2=4x, 3=6x, 4=8x, 5-7=reserved) |
| **`0x0800`** | (reserved) |
| **`0x3000`** | Pre-FEC Padding Factor |
| **`0x4000`** | TxBF |
| **`0x8000`** | PE Disambiguity |

## data 6

| **`0x000f`** | NSTS (actual number of space-time streams, 0=unknown, 1=1, etc.) |
| **`0x0010`** | Doppler value |
| **`0x00e0`** | (reserved) |
| **`0x7f00`** | TXOP value |
| **`0x8000`** | midamble periodicity (0=10, 1=20) |
