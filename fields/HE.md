---
title: HE
categories: [suggested]
---
Bit Number
: not assigned yet

Structure
: - u32 sig_A1
  - u32 sig_A2
  - u16 sig_A1_known
  - u16 sig_A2_known

Required Alignment
: 4

Unit(s)
: none

The presence of this field indicates that the frame was received or
transmitted using the HE PHY.

This field contains the HE-SIG-A part that is common to all HE transmissions.
If the transmission format was HE_MU, the [HE-MU-common](HE-MU-common) field
should also be present. At the very least, the [HE-MU-user](HE-MU-user)
field needs to be present once for an HE_MU frame since it indicates the
user bandwidth.

## sig_A1

| **`0x03ffffff`** | Bits 0-25 of the SIG-A1 field |
| **`0x3c000000`** | reserved |
| **`0xc0000000`** | non-spec, HE Format: 0=HE_SU, 1=HE_EXT_SU, 2=HE_MU, 3=HE_TRIG |

TODO: add the three formats for information

## sig_A2

| **`0x03ffffff`** | Bits 0-25 of the SIG-A2 field |
| **`0xfc000000`** | reserved |

TODO: add the three formats for information

## sig_A1_known

| **flag**     | **HE SU PPDU meaning** | **HE MU PPDU meaning** | **HE trigger-based PPDU meaning** |
| **`0x0001`** | Format                 | UL/DL                  | Format                            |
| **`0x0002`** | Beam Change            | SIG-B MCS              | BSS Color                         |
| **`0x0004`** | UL/DL                  | SIG-B DCM              | Spatial Reuse 1                   |
| **`0x0008`** | MCS                    | BSS Color              | Spatial Reuse 2                   |
| **`0x0010`** | DCM                    | Spatial Reuse          | Spatial Reuse 3                   |
| **`0x0020`** | BSS Color              | Bandwidth              | Spatial Reuse 4                   |
| **`0x0040`** | B14                    | # of HE-SIG-B Sym/Usrs | B23 (Reserved)                    |
| **`0x0080`** | Spatial Reuse          | SIG-B Compression      | Bandwidth                         |
| **`0x0100`** | Bandwidth              | GI+LTF Size            | (reserved)                        |
| **`0x0200`** | GI+LTF size            | Doppler                | (reserved)                        |
| **`0x0400`** | Nsts                   | (reserved)             | (reserved)                        |
| **`0xf800`** | (reserved)             | (reserved)             | (reserved)                        |

## sig_A2_known

| **flag**     | **HE SU PPDU meaning** | **HE MU PPDU meaning** | **HE trigger-based PPDU meaning** |
| **`0x0001`** | TXOP Duration          | TXOP Duration          | TXOP Duration                     |
| **`0x0002`** | Coding                 | B7 (Reserved)          | B7 (Reserved)                     |
| **`0x0004`** | LDPC Extra Sym Seg     | # of HE-LTF Symbols    | B8 (Reserved)                     |
| **`0x0008`** | STBC                   | LPDC Extra Symbol      | B9 (Reserved)                     |
| **`0x0010`** | TxBF                   | STBC                   | B10 (Reserved)                    |
| **`0x0020`** | Pre-FEC Padding Factor | Pre-FEC Padding Factor | B11 (Reserved)                    |
| **`0x0040`** | PE Disambiguity        | PE Disambiguity        | B12 (Reserved)                    |
| **`0x0080`** | B14 (Reserved)         | (reserved)             | B13 (Reserved)                    |
| **`0x0100`** | Doppler                | (reserved)             | B14 (Reserved)                    |
| **`0x0200`** | (reserved)             | (reserved)             | B15 (Reserved)                    |
| **`0x0400`** | CRC                    | CRC                    | CRC                               |
| **`0x0800`** | Tail                   | Tail                   | Tail                              |
| **`0xf000`** | (reserved)             | (reserved)             | (reserved)                        |
