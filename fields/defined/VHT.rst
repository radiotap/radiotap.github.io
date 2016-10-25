VHT
===

Bit Number  21

Structure  u16 known, u8 flags, u8 bandwidth, u8 mcs_nss[4], u8 coding, u8 group_id, u16 partial_aid

Required Alignment  2

The ``known`` field indicates which information is known:

[Table not converted]

The ``flags`` field is any combination of the following:

[Table not converted]

The ``bandwidth`` field encodes the bandwidth:

[Table not converted]

Note: for receive capture, the total bandwidth of the transmitter is not generally known, so the bandwidth will only be recorded as 20, 40, 80, or 160.

Note: for transmit injection, the sub-band choice for wide channels may be constrained by the current primary sub-band channels. IEEE 802.11 prohibits transmissions on sub-bands other than the designated sub-bands. For example, if the device is currently operating on the 40MHz channel pair {36, 40} with 36 designated as the primary 20MHz channel, the transmitter will naturally send 20MHz transmissions on channel 36, and may not be able to force a 20MHz transmission on channel 40.

Bandwidth values are:

[Table not converted]

The four ``mcs_nss`` fields encode MCS and NSS for up to four users:

[Table not converted]

If the NSS field for a user is zero, the user is not present and the MCS and coding (in the coding field) associated with that user are not valid. If the NSS field for a user is non-zero, but the MCS is not known (for example due to receiving only data for a single user), the MCS shall be set to 15. For SU PPDUs, only the first user will have a nonzero NSS field.

Note: the number of space-time streams (NSTS) for a user can be calculated from the NSS for that user and the STBC flag:

* STBC not in use: NSTS = NSS

* STBC in use: NSTS = 2*NSS

The ``coding`` field encodes the FEC for up to four users:

[Table not converted]

The coding for a user is only valid if the NSS (in the ``mcs_nss`` field) for that user is nonzero.

The ``group_id`` field contains the group ID.

Note: the group ID can be used to differentiate between SU PPDUs (group ID is 0 or 63) and MU PPDUs (group ID is 1 through 62).

The ``partial_aid`` field contains the partial AID. Only applicable to SU PPDUs.

