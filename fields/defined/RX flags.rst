RX flags
========

Bit Number  14

Structure  u16

Required Alignment  2

Unit  bitmap

Properties of received frames.

The following flags are currently defined:

[Table not converted]

Notes
=====

This field originates from NetBSD and is also used like this in Linux.

Use bit ``0x40`` in the `flags field`_ to indicate *FCS CRC failed*.

.. ############################################################################

.. _flags field: ../Flags

