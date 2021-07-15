---
title: Software
layout: default
group: software
---

# Software

---

## Crystallographic software available on the beamline computers

### XDS

Is available for [download](https://xds.mr.mpg.de/html_doc/downloading.html) from the
[XDS project page](https://xds.mr.mpg.de) at the MPI for Medical Research, Heidelberg.

XDS is available on all beamline computers at 8.3.1 but we recommend that you run your XDS jobs on
`octamus1` which can be accessed via `ssh` from the gateway. We have recently configured a queueing
system on octamus1 so you should be able to launch your jobs from any beamline computer and they
will be actually run on `octamus1` ... I think.

[XDS Documentation](https://xds.mr.mpg.de/html_doc/XDS.html)

### CCP4

Is available for [download](https://www.ccp4.ac.uk/download) from [CCP4](https://www.ccp4.ac.uk)

All CCP4 programs are available on all beamline computers.

[CCP4 Documentation](https://www.ccp4.ac.uk/?page_id=200)

### DIALS

Is available for [download](https://dials.github.io/installation.html) from the
[DIALS](https://dials.github.io) webpage or from [GitHub](https://github.com/dials/dials).

### autoPROC

Requires a license so probably better to just use the version we have installed. It should work on
any beamline computer, but keep in mind that it is using XDS and CCP4 under teh hood so should be
run on computers other than teh gateway.

[autoPROC Documentation](https://www.globalphasing.com/autoproc/manual/index.html)

### Xia2

Is now distributed with DIALS.

[Xia2 Documentation](https://xia2.github.io)

---

## Our projects hosted on GitHub and GitLab

Beamline 8.3.1 [GitHub](https://github.com/bl831) organization.  
Beamline 8.3.1 [GitLab](https://git.bl831.als.lbl.gov) server for internal projects.  
