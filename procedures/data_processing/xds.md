---
title: XDS Data Processing
layout: default
group: data_processing
---

# Processing data with XDS at 8.3.1

---

From Holton on Dec. 14, 2016, re: processing fresh data while at ALS 8.3.1:

It's not exactly ready for prime time, but it's called **xds_rollup.com**.
You point it at one or more root directories and it runs xds_runme.com
on each. The result can be a bit of a mess, with different space groups
and sub-groups represented, different indexing conventions etc all over,
but at least the processing is organized into chronologically ordered
"wedge" directories under the directory where you launch it. It is
designed to run over-and-over again, adding wedges as you go. It will
also try to re-run every wedge in P1 (for reference) and also use DIALS.

Cleaning up the mess is still more of a work in progress.
*~jamesh/Develop/xds_followup_notes.com* is an attempt to try to
clean up the mess. Every possible re-indexing operator between every pair
of wedges is enumerated, applied, and an R-factor calculated. The
minimum-R connections can then be grouped into clusters, and re-indexed
into potentially compatible merging groups. It takes a very very long
time, proportional to the square of the number of data sets. But it is
the only general solution to the problem.

## Practically speaking

From the `gateway` (if logged in via NX) or `graphics3` (if logged in at the beamline).

```bash
ssh dataserver4
cd /home/mcfuser/yourorganization/yourusername/ddMMMyyyy/
mkdir xds_rollup
cd xds_rollup
xds_rollup.com /data/mcfuser/ucsf/keedy/ddMMMyyyy/
```

This will continue forever. Can kill whenever, then restart later (presumably in same way, but when logged in remotely).
