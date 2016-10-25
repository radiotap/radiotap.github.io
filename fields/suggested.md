---
title: Suggested Fields
layout: suggested
---
Note that some fields currently have numbers assigned already,
this is due to different OSes defining different bits unilaterally. Such
mistakes should not be repeated in the future. However, even though
there are vendor namespaces, you should resist the temptation to define
globally useful fields in your own vendor namespace and propose them for
standardisation instead.

This table lists the fields some OSes assigned by bit number:


| **bit number** | **field** |
| 14 | [FCS in header](/fields/FCS in header) (clashes with official assignment) |
| 15 | [TX flags](/fields/TX flags), [hardware queue](/fields/hardware queue) |
| 16 | [RTS retries](/fields/RTS retries), [RSSI](/fields/RSSI) |
| 17 | [data retries](/fields/data retries) |
| 18 | [XChannel](/fields/XChannel) |
