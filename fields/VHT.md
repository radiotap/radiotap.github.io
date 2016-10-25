---
title: VHT
categories: [defined]
---
Bit Number
: 21

Structure
: u16 known, u8 flags, u8 bandwidth, u8 mcs\_nss\[4\], u8
coding, u8 group\_id, u16 partial\_aid

Required Alignment
: 2

The `known` field indicates which information is known:

| **flag** | **definition** | **notes** |
| 0x0001 | STBC known|In `flags` part of the field. |
| 0x0002 | TXOP_PS_NOT_ALLOWED known|In `flags` part of the field. |
| 0x0004 | Guard interval|In `flags` part of the field. |
| 0x0008 | Short GI NSYM disambiguation known|In `flags` part of the field. |
| 0x0010 | LDPC extra OFDM symbol known|In `flags` part of the field. |
| 0x0020 | Beamformed known/applicable|In `flags` part of the field. This flag should be set to zero for MU PPDUs. |
| 0x0040 | Bandwidth known|In `bandwidth` part of the field. |
| 0x0080 | Group ID known|In `group_id` part of the field. |
| 0x0100 | Partial AID known/applicable|In `partial_aid` part of the field. This flag should be set to zero for MU PPDUs. |
| 0xfe00 | (unused) | |

The `flags` field is any combination of the following:

| **flag** | **definition** | **notes** |
|0x01|STBC|Space-time block coding.<<BR>>Set to 0 if no spatial streams of any user has STBC.<<BR>>Set to 1 if all spatial streams of all users have STBC.|
|0x02|TXOP_PS_NOT_ALLOWED|Valid only for AP transmitters.<<BR>>Set to 0 if STAs may doze during TXOP.<<BR>>Set to 1 if STAs may not doze during TXOP or transmitter is non-AP.|
|0x04|Guard interval.|Set to 0 for long GI.<<BR>>Set to 1 for short GI.|
|0x08|Short GI NSYM disambiguation|Valid only if short GI is used.<<BR>>Set to 0 if NSYM mod 10 != 9 or short GI not used.<<BR>>Set to 1 if NSYM mod 10 = 9. |
|0x10|LDPC Extra OFDM symbol|Set to 1 if one or more users are using LDPC and the encoding process resulted in extra OFDM symbol(s).<<BR>>Set to 0 otherwise.|
|0x20|Beamformed|Valid for SU PPDUs only.|
|0xc0|(unused)| |

The `bandwidth` field encodes the bandwidth:

| **bitmask** | **definition** | **notes** |
|0x1f|Bandwidth| |
|0xe0|(unused)| |

Note: for receive capture, the total bandwidth of the transmitter is not
generally known, so the bandwidth will only be recorded as 20, 40, 80,
or 160.

Note: for transmit injection, the sub-band choice for wide channels may
be constrained by the current primary sub-band channels. IEEE 802.11
prohibits transmissions on sub-bands other than the designated
sub-bands. For example, if the device is currently operating on the
40MHz channel pair {36, 40} with 36 designated as the primary 20MHz
channel, the transmitter will naturally send 20MHz transmissions on
channel 36, and may not be able to force a 20MHz transmission on channel
40.

Bandwidth values are:

| **value** | **total bandwidth (MHz)** | **sideband** | **sideband index** |
| 0 | 20 |   |   |
| 1 | 40 |   |   |
| 2 | 40 | 20L | 0 |
| 3 | 40 | 20U | 1 |
| 4 | 80 |   |   |
| 5 | 80 | 40L | 0 |
| 6 | 80 | 40U | 1 |
| 7 | 80 | 20LL | 0 |
| 8 | 80 | 20LU | 1 |
| 9 | 80 | 20UL | 2 |
| 10 | 80 | 20UU | 3 |
| 11 | 160 |   |   |
| 12 | 160 | 80L | 0 |
| 13 | 160 | 80U | 1 |
| 14 | 160 | 40LL | 0 |
| 15 | 160 | 40LU | 1 |
| 16 | 160 | 40UL | 2 |
| 17 | 160 | 40UU | 3 |
| 18 | 160 | 20LLL | 0 |
| 19 | 160 | 20LLU | 1 |
| 20 | 160 | 20LUL | 2 |
| 21 | 160 | 20LUU | 3 |
| 22 | 160 | 20ULL | 4 |
| 23 | 160 | 20ULU | 5 |
| 24 | 160 | 20UUL | 6 |
| 25 | 160 | 20UUU | 7 |

The four `mcs_nss` fields encode MCS and NSS for up to four users:

| **bitmask** | **definition** | **notes** |
|0x0f|NSS|Number of spatial streams, range 1-8.|
|0xf0|MCS|MCS rate index, range 0-9.|

If the NSS field for a user is zero, the user is not present and the MCS
and coding (in the coding field) associated with that user are not
valid. If the NSS field for a user is non-zero, but the MCS is not known
(for example due to receiving only data for a single user), the MCS
shall be set to 15. For SU PPDUs, only the first user will have a
nonzero NSS field.

Note: the number of space-time streams (NSTS) for a user can be
calculated from the NSS for that user and the STBC flag:

-   STBC not in use: NSTS = NSS
-   STBC in use: NSTS = 2\*NSS

The `coding` field encodes the FEC for up to four users:

| **bitmask** | **definition** | **notes** |
|0x01|Coding for user 0|Set to 0 for BCC.<<BR>>Set to 1 for LDPC.|
|0x02|Coding for user 1|Set to 0 for BCC.<<BR>>Set to 1 for LDPC.|
|0x04|Coding for user 2|Set to 0 for BCC.<<BR>>Set to 1 for LDPC.|
|0x08|Coding for user 3|Set to 0 for BCC.<<BR>>Set to 1 for LDPC.|
|0xf0|(unused)| |

The coding for a user is only valid if the NSS (in the `mcs_nss` field)
for that user is nonzero.

The `group_id` field contains the group ID.

Note: the group ID can be used to differentiate between SU PPDUs (group
ID is 0 or 63) and MU PPDUs (group ID is 1 through 62).

The `partial_aid` field contains the partial AID. Only applicable to SU
PPDUs.
