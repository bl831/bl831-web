---
title: Data Processing with Xia2
layout: default
group: data_processing
---

# Processing data with Xia2 at 8.3.1

---

Detailed [documentation](https://www.globalphasing.com/autoproc/manual/index.html) can be found on
the [Global Phasing](https://www.globalphasing.com) website.

## Practically speaking (guidance yanked from the [Xia2](https://xia2.github.io/quick_start.html) web page)

From the `gateway` (if logged in via NX) or `graphics3` (if logged in at the beamline).

If you don’t like reading manuals and just want to get started, try:

```bash
xia2 pipeline=dials /here/are/my/images
```

or:

```bash
xia2 pipeline=3d /here/are/my/images
```

(remembering of course `atom=X` if you want anomalous pairs separating in scaling.)
If this appears to do something sensible then you may well be home and dry. Some critical options:

If this doesn’t hit the spot, you’ll need to read the rest of the [documentation](https://xia2.github.io/parameters.html).

| Option | Usage |
| ------ | ----- |
| atom=X | tell xia2 to separate anomalous pairs i.e. I(+) ≠ I(−) in scaling|
| pipeline=dials | tell xia2 to use DIALS |
| pipeline=dials-aimless | tell xia2 to use DIALS and Aimless |
| pipeline=3d | tell xia2 to use XDS and XSCALE |
| pipeline=3dii | tell xia2 to use XDS and XSCALE, indexing with peaks found from all images |
