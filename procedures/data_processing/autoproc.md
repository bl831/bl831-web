---
title: Data Processing with autoPROC
layout: default
group: data_processing
---

# Processing data with Global Phasing autoPROC at 8.3.1

---

Detailed [documentation](https://www.globalphasing.com/autoproc/manual/index.html) can be found on
the [Global Phasing](https://www.globalphasing.com) website.

## Practically speaking

From the `gateway` (if logged in via NX) or `graphics3` (if logged in at the beamline).

The recommended way to run autoPROC is the command

```process -I /where/ever/images -d out > out.log```

This will define where the images are, where output files (subdirectory "out") and message (to file "out.log") should go. If the information in the header of the images is correct (which it should be) - this is all that's needed. You can also run the command within a directory containing images (in which case the -I flag is not required) or have it create output files and directories within the current directory - it all depends on the directory layout you use and want to enforce for data-processing.

It is always a good idea to let autoPROC write all output into a separate sub-directory:

```process -d <dir>```

(where `<dir>` could be e.g. `01` to get sequential numbering if several runs are going to be done).
We would also recommend saving standard output via

```process -d <dir> > dir.log```
