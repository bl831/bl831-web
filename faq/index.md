---
title: ALS 8.3.1 FAQ
layout: default
group: faq
---

# FAQ

---
## General guidelines:

* Do whatever makes sense to you
* To minimize training, we are trying to organize the beamline so that following your intuition will have the desired outcome.  If it doesn't I'd like to hear about it.
* Do not delete your data. That is my job. We do systemwide archives on Mondays so that you will always have a copy of your data at the beamline. We also do statistics on data collection to try and improve the user-friendliness of the beamline.
* Do not compress your data. Compressed files still take up space and are impossible to process. They are not good for anything. If you want to compress files for transfer, have a look at moving data around for better ways to do this.
* Do your processing in `/home`, not `/data`. Processing onto the data disk slows down data collection and takes up a lot of space. The `/data` disk is optimized for large files. Lots of small files can fill up `/data` at only ~75% of its full capacity!

## How do I acknowledge beamline 8.3.1 in my paper?

> Beamline 8.3.1 at the Advanced Light Source is operated by the University of California Office of the President, Multicampus Research Programs and Initiatives grant MR-15-328599 the National Institutes of Health (R01 GM124149 and P30 GM124169),Plexxikon Inc. and the Integrated Diffraction Analysis Technologies program of the US Department of Energy Office of Biological and Environmental Research. The Advanced Light Source (Berkeley, CA) is a national user facility operated by Lawrence Berkeley National Laboratory on behalf of the US Department of Energy under contract number DE-AC02-05CH11231, Office of Basic Energy Sciences. </p> </blockquote>

## Where are the BL8.3.1 Status and Schedule pages?

Right here: [BL8.3.1 Status Page](/beamline/status/) and here: [BL8.3.1 Schedule](/beamline/schedule/)

## What is the meaning of life?

[42](https://en.wikipedia.org/wiki/42_(number)#The_Hitchhiker's_Guide_to_the_Galaxy)

## How do I start Blu-Ice?

type `go` in a terminal window.

## What is this Blu-Ice thing anyways?

Blu-Ice is software you will use to control the beamline and collect your data. The version used at
8.3.1 is very similar to the version originally developed and deployed at by
[SMB](https://www-ssrl.slac.stanford.edu/smb/) at SSRL, and reading the
[Blu-Ice manual](https://smb.slac.stanford.edu/facilities/software/blu-ice/) can be quite
instructive ([RTFM](https://en.wikipedia.org/wiki/RTFM))

## Where's the ADXV image display?

It should appear in the upper right of your Linux Desktop when you launch Blu-Ice with the `go`
command. However, if it is missing or you want a second instance you can click on `Open With` at
bottom right of the Blu-Ice image display on the HUTCH Tab, and select `ADXV`.

## I can't collect data, what do I do?

If the ALS up and running, and the beamline is not working, call "x2249" from the Beamline phone.

## How do I get a strategy?

Type `index` and the Elves will guide you through it.

## How do I process my data set?

Processing will begin automatically as soon as you start collecting a data set.
A new terminal, opened to our fastest computer, dataserver4, will appear on your desktop.
XDS will be running, with Pointless and Aimless to follow, if XDS is sucessfull.

## I need more Info on Data Collection, Processing, and Scripts?

Click [HERE](http://bl831.als.lbl.gov/~gmeigs/useful_scripts.html)

## How do I get my data home?

Click [HERE](http://bl831.als.lbl.gov/~gmeigs/data_backup.html) For portable Hard Drives and Network options,

## What do I do before I leave?

  CLOSE HUTCH DOOR!   -and-   TURN PHOTONS ON!
... Then, type "finished". This will set up the beamline to it's default state:
cryojet.com on; wave.com 11111; divergence.com 2 X .35; reset_runs.com nextuser
... and trigger a write of your last data DVD, if you had requested them.

## Any other best practices I should be aware of?

Do not interfere with other people's beam time
If you are doing processing after your beam time, try to remember to restrict your CPU activity to "crush17." Do NOT restore any files to /data unless you know how to preserve their date stamps. Image files with new dates will be mistaken for newly-collected data and mess up the automatic archiver.

## Do you have HKL2000?

We don't have HKL2000 at 8.3.1. [XDS](https://xds.mr.mpg.de) and [DIALS](https://dials.github.io)
get great results with Pilatus data. I'm working with ZO and others to test HKL2000 on our data
stream, but I think in the immediate future you'll probably be happiest with XDS processing.

## Any opinions about what to look for when evaluating a beamline?

Oh yes... What you really want to look at when evaluating a beam's performance for MX is four things:
1. flux in photons/s.  This determines how long it takes to do an experiment before the crystal is dead. The problem with flux as a metric, however, is that people cheat, so there are caveats.
2. beam size. should be matched to your crystal size if at all possible.  Most beamlines quote their flux with no aperture at the sample, which is cheating because that means not all of it is hitting your crystal. For example, APS 19-ID quotes 1.3e13 photons/s/mm^2, which means the flux into their focused beam size of 0.02 x 0.1 mm is 2.6e10 photons/s, which is 10x lower than 8.3.1.
3. divergence is the main advantage of insertion devices over bends. Undulators are natively low-divergence sources, so you don't have to think about it.  With bends (and superbends) you can "cheat" and get more flux by opening up the divergence.  This comes at the expense of spreading out the spots, but if you're careful you can stay below the threshold where divergence affects your data.  At all ALS beamlines the divergence is adjustable, and default settings (1-2 mrad) are such that you will not see any impact on your data unless you have a large cell and move the detector to more than ~300 mm.  For our ribosome users we cut divergence down to 0.5 mrad.  There is proportionally less flux, but you can compensate with 4x longer exposures.  The resulting data quality is the same, just takes longer to collect.  
4. dispersion. another way to "cheat" is to use a multilayer monochromator.  These give orders of magnitude more flux, but at the expense of spreading out and fading high-resolution spots into the background. We have two ML-capable beamlines at ALS (12.3.1 and 8.2.1).  This can be useful for screening, but for high-resolution data collection you want to switch back to the silicon-111 crystals (which can be done in 5-15 minutes).  8.3.1 has a silicon-111 mono.

One final thing to bear in mind is radiation damage.  You can't outrun it.  Well, XFELs can, but not synchrotrons.  Because of this, the number of photons you get onto your detector before the crystal is dead is fixed.  It's about 1e6 scattered photons per cubic micron of crystal.  So, when you're at any beamline the only thing you get to decide is how many images to put those photons on.  We have software that will suggest an optimal solution.  Your choice of beamline affects how long it will take to get those photons.  At 8.3.1 its 5 minutes.  Beyond the beam, the most important things are how well maintained the hardware is, how feature-filled the software is, and how good the user support will be.  I'd like to think 8.3.1 is competitive on the first and leads the world on those last three.
