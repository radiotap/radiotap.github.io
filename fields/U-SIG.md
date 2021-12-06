---
title: U-SIG
categories: [suggested]
---
Type
: 33

Structure
- u32 common
- u32 value, mask

Required Alignment
: 4

Unit(s)
: none

This field indicates the (known) contents of the U-SIG.

Note that the common/value/mask fields are ordered in this way
so if they're all known, the U-SIG bits are all contiguous in
memory in the same way as over the air from bit 12 of the common
field to the end of the value field.

## common

| **`0x00000001`** | PHY version identifier known |
| **`0x00000002`** | BW known |
| **`0x00000004`** | UL/DL known |
| **`0x00000008`** | BSS Color known |
| **`0x00000010`** | TXOP known |
| **`0x00000fe0`** | (reserved) |
| **`0x00007000`** | PHY version identifier |
| **`0x00038000`** | BW |
| **`0x00040000`** | UL/DL |
| **`0x01f80000`** | BSS Color |
| **`0xfe000000`** | TXOP |

## value / mask

Contains a known mask and value for the remaining U-SIG bits
that can only be interpreted depending on the PHY version.

The bits are in the on-air order, i.e. U-SIG-1 `B20-25` followed
by U-SIG-2 `B0-25`. Thus, U-SIG-1 `B20-25` are in `mask` and
`value` bits `0x0000003f`.

Dissectors should show these per spec, in a PHY version specific
namespace (e.g. "U-SIG::EHT::PPDU-Type-And-Compression-Mode").

For the only currently defined version (PHY Version identifier 0
for EHT), the bits are shown in the following tables:

### EHT MU PPDU U-SIG contents

An EHT PPDU is an EHT MU PPDU if
* the UL/DL field is set to 0 and the PPDU Type And Compression Mode field is set to 0, 1 or 2;
* the UL/DL field is set to 1 and the PPDU Type And Compression Mode field is set to 1.

| **bits**         | **U-SIG reference** | **Content** |
| **`0x0000001f`** | `U-SIG-1 B20-B24`   | Disregard (all ones) |
| **`0x00000020`** | `U-SIG-1 B25`       | Validate (must be 1) |
| **`0x000000c0`** | `U-SIG-2 B0-B1`     | PPDU Type And Compression Mode |
| **`0x00000100`** | `U-SIG-2 B2`        | Validate (must be 1) |
| **`0x00003e00`** | `U-SIG-2 B3-B7`     | Punctured Channel Information |
| **`0x00004000`** | `U-SIG-2 B8`        | Validate (must be 1) |
| **`0x00018000`** | `U-SIG-2 B9-B10`    | EHT-SIG MCS |
| **`0x003e0000`** | `U-SIG-2 B11-B15`   | Number Of EHT-SIG Symbols |
| **`0x03c00000`** | `U-SIG-2 B16-B19`   | CRC (for the bits `U-SIG-1 B0` to `U-SIG-2 B15`) |
| **`0xfc000000`** | `U-SIG-2 B20-B25`   | Tail (must be 0) |

### EHT TB PPDU U-SIG contents

An EHT PPDU is a EHT TB PPDU if
* the UL/DL field is set to 1 and the PPDU Type And Compression Mode field is set to 0.

| **bits**         | **U-SIG reference** | **Content** |
| **`0x0000003f`** | `U-SIG-1 B20-B25`   | Disregard (all ones) |
| **`0x000000c0`** | `U-SIG-2 B0-B1`     | PPDU Type And Compression Mode |
| **`0x00000100`** | `U-SIG-2 B2`        | Validate (must be 1) |
| **`0x00001e00`** | `U-SIG-2 B3-B6`     | Spatial Reuse 1 |
| **`0x0001e000`** | `U-SIG-2 B7-B10`    | Spatial Reuse 2 |
| **`0x003e0000`** | `U-SIG-2 B11-B15`   | Disregard (...) |
| **`0x03c00000`** | `U-SIG-2 B16-B19`   | CRC (for the bits `U-SIG-1 B0` to `U-SIG-2 B15`) |
| **`0xfc000000`** | `U-SIG-2 B20-B25`   | Tail (must be 0) |
