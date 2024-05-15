---
title: extended flags
categories: [suggested]
type: 22
---
Bit Number
: 22 (not assigned yet)

Structure
: u32 flags

Required Alignment
: 4

Unit(s)
: n/a

This field defines decryption flags for frames. The following flags are
defined:

| **value** | **meaning** |
| `0x00000001` | frame is decrypted (but FC protected bit is set) |
| `0x00000002` | frame is encrypted (FC protected bit is also set) |
| `0x00000004` | (ext) IV is still present (reserved if 0x1 isn't set) |
| `0x00000008` | MIC is not present (should only be used if FCS is also not present, reserved if 0x1 isn't set) |
| `0xfffffff0` | (reserved) |
