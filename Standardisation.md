---
title: Standardisation
---
The radiotap community broadly agreed on this process for adding new
fields to radiotap. New fields should be generally useful to everybody
using radiotap.

The process:

1.  Define the bit number, alignment, width, interpretation of the
    fields on [the suggested fields page](../suggested-fields).
2.  Produce implementations wireshark and/or tcpdump and for one or
    more drivers.
3.  Post the field definition and patches (the code) on the list.
4.  Leave at least three weeks for discussion.
5.  If the proposal withstands discussion, re-post proposal in final
    form; otherwise start from the beginning.
6.  Adopt the proposal in one week if there are no further objections
    (discussion is over, however, another week lets everyone verify that
    the proposal and amendments, as discussed, have become the
    standard); make the necessary wiki/spec changes.
