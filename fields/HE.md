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
  - u8 sig_B_common_RU[4]
  - u16 sig_B_common
  - u16 sig_B_common_known
  - u32 sig_B_user1

Required Alignment
: 4

Unit(s)
: none

The presence of this field indicates that the frame was received or
transmitted using the HE PHY.

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
| **`0x0010`** | Center 26-tone RU bit is known (if present at all) |
| **`0x0020`** | CRC field value is known |
| **`0x0040`** | Tail field value is known |
| **`0xFF80`** | (reserved) |

## sig_B_user1

| **`0x001fffff`** | HE-SIG-B user field as in spec |
| **`0x000007ff`** | STA-ID |
| **`0x00003800`** | NSTS |
| **`0x00004000`** | Tx Beamforming |
| **`0x00078000`** | MCS |
| **`0x00080000`** | DCM |
| **`0x00100000`** | Coding |
| **`0x00e00000`** | (reserved) |
| **`0x01000000`** | user field position known |
| **`0x02000000`** | the captured MPDU is for this user |
| **`0x04000000`** | STA-ID known |
| **`0x08000000`** | NSTS known |
| **`0x10000000`** | Tx Beamforming known |
| **`0x20000000`** | MCS known |
| **`0x40000000`** | DCM known |
| **`0x80000000`** | Coding known |

This field contains the first or the captured (or both) user field. If the
"user field position known" bit is set, then this field contains the first
User field from the HE-SIG-B User Specific fields, which may not have been
the user field for which the captured MPDU (that this radiotap header is
attached to) was received. In this case, the [HE multiuser](HE multiuser)
field shall be present in the radiotap header as well.
