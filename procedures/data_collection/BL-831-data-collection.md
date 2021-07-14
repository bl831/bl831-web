---
title: BL 8.3.1 Data Collection
layout: default
group: data_collection
---

# BL 8.3.1 Data Collection
---
Some good advice in this article:

http://journals.iucr.org/d/issues/2013/07/00/ba5199/ba5199.pdf



this is a work in progress - I've changed it quite a bit recently, so don't blindly accept all of the information below. this notice will be removed when I have time to fix it.

The usual disclaimers apply - rely on experts, not sleep-deprived grad students. The information below has worked well for me in the past but is not necessarily universally applicable. In all matters, consult James Holton first, especially on details specific to this beamline; much of what follows is based on his answers (and Ho's, and Tom's) to my endless questions.

Disclaimer #2: I usually work with crystals that diffract well to high resolution, and my experience with experimental phasing is less extensive. However, I've tried to make this as thorough as possible.

Sections that look like this go into way more detail and can be ignored if you're in a hurry.
Contents [hide]
1 Pre-collection setup
2 Test shots
3 Indexing and determining a strategy
3.1 The "index" script
3.2 What the strategy means
3.3 Figuring out the real lattice
4 Other parameters.
5 MAD/SAD data collection
[edit]Pre-collection setup
Running the script tuneup.com is recommended whenever changing the energy significantly (e.g. closer to the absorption edge of a particular atom, or by more than several hundred eV), and after every storage ring refill.

Depending on the size of your crystals, you may want to change the collimator (basically the pinhole that controls final beam width). The default is 100 microns, but if your crystals are significantly smaller you'll want to use the 50 or 30 micron collimators. This will reduce flux proportional to the reduction in the area of the cross-section, so unless you want to limit the area of the crystal exposed to the beam you would normally leave the 100um in place for decent-sized crystals, but it is essential for limiting noise when shooting small crystals. This is somewhat involved but fortunately well documented.

[edit]Test shots
Although it's often possible to index off a single diffraction image, it works better if you have at least two images. On James' recommendation, I collect these at right angles to each other, i.e. take one shot, rotate the image 90 degrees, and take another shot. Since I get very thin plates a lot, I always collect one shot with the beam normal to the face, and the other directly through the edge. This has the advantage of telling me if the diffraction is anisotropic to any degree.

My plate crystals vary widely in quality, and a significant majority have pathologies when shot through the edge. Although this sometimes just means a slight drop in resolution, more often I see smearing of spots and/or a large drop in resolution. I've been able to use images that were slightly smeared, but unfortunately the majority were clearly unusable. If Elves can index the images, it's probably worth collecting data.
[edit]Indexing and determining a strategy
The Elves manual covers some of this in more detail, but I've interleaved it with tidbits picked up from conversations with James and my own repeated failures.

Indexing is the first stage of data processing: determining the initial lattice parameters from the positions of spots on the diffraction pattern. Hopefully this will go well and provide you with a clear choice (or choices) for the lattice. At the beamline, this is always done with Elves; therefore, I'm going to cover the process completely (except for strategization, it will apply for post-collection processing as well). After you select an appropriate lattice, Elves will determine the collection strategy based on the crystal orientation and requirements for this particular lattice. At the end, it will automatically set up a collection run in the main graphical window.

[edit]The "index" script
Once you have taken a couple (or more) test shots, you can use Elves to calculate the optimal data collection parameters for your crystal. This is done on the command line:

   mcfuser@crush04 % index
If you have multiple (usually two) frames of the same crystal with only the phi angle changed - this is the ideal case - you invoke index with the first frame in the series, and it will automatically use subsequent frames as well. Typing just index at the prompt will cause it to use only the most recent images; Elves will try to auto-detect which new frames go together; this will be wrong if the crystal position has changed, but you can force it to use all appropriate frames by explicitly naming the first image in the series:

   mcfuser@crush04 % index /data/mcfuser/alber/nat/lysozyme_0_001.img
It is difficult and/or pointless to try to index by eye. However, there are some hints you can get from the diffraction pattern - a trigonal or hexagonal lattice will be obvious from the spots. Tom can tell whether a lattice is F- or I-centered based on patterns in the intensities. Aside from this, you can drag the mouse across spots in the same lattice line in ADXV and it will tell you the approximate real-space difference between them.
You should be able to simply hit Return for the next few prompts until you reach the point of autoindexing. You do not want to use graphics unless absolutely necessary (that's another tutorial altogether). After Elves indexes (assuming MOSFLM doesn't choke on the data), it will print something like this:

 example      distortion
 space group  of cell  unit cell
 P3           0.190     37.55    38.44    77.27  89.6  90.4 118.6
                        37.99    37.99    77.27  90.0  90.0 120.0
 P4           1.010     37.55    38.44    77.27  89.6  90.4 118.6
                        37.99    37.99    77.27  90.0  90.0  90.0
 F222         1.870     37.55    67.49   158.78  89.7 103.3  90.6
                        37.55    67.49   158.78  90.0  90.0  90.0
 C2221        0.090     37.55    67.49    77.27  89.8  90.4  89.4
                        37.55    67.49    77.27  90.0  90.0  90.0
 P222         0.930     37.55    38.44    77.27  89.6  90.4 118.6
                        37.55    38.44    77.27  90.0  90.0  90.0
 C2           0.060     37.55    67.49    77.27  89.8  90.4  89.4
                        37.55    67.49    77.27  90.0  90.4  90.0
 P2           0.060     37.55    77.27    38.79  90.0 119.6  90.4
                        37.55    77.27    38.79  90.0 119.6  90.0
 P1           0.000     37.55    38.44    77.27  89.6  89.6  61.4
                      37.55    38.44    77.27  89.6  89.6  61.4
 What is your space group? [P3]
The "distortion of cell" statistic immediately rules out the orthorhombic and tetragonal lattices in this case. Note that P1 is always the highest-scoring option, because there are no constraints on cell edges or angles. In this case, Elves suggests P3 because it's the highest-symmetry lattice with a good score. (For the curious and/or confused, HKL2000 has a slightly different output with more choices by default, but it basically means the same thing.)

There are several weird details here. One is that there may be multiple equally good lattices with different dimensions, picked from the same spots (e.g. P2 and C2221 solutions will always have different unit cell lengths). Don't worry too much about this for now. One problem that arises occasionally is that the order of unit cell axes may be pre-determined in some cases but variable in others. For instance, I've had crystals with a P2 lattice that had all angles almost exactly equal to 90. However, in P2 the beta angle is unconstrained. Which orientation we choose for the cell - that is, which angle becomes beta - is extremely important, but the program can easily get it wrong in these cases. In Mosflm this is easy to fix; in HKL2000 it's much harder.
It should be obvious by now that "lattice" (or "point group") and "space group" don't mean the same thing. At this stage the software only cares about where to look for spots on the images, and this is determined by lattice type. This means that screw axes are irrelevant at this point (e.g. there is no difference between P222 and P212121 as far as we're concerned), and some of the higher-symmetry space groups are indexed as lower-symmetry initially (i.e. I4 and I422 are treated identically for now, as are P3 and P6). We'll deal with space groups when we get to scaling.

I tend towards the paranoid when indexing a new crystal form, because I've had bad experiences with picking the wrong lattice and ending up with too little data. In one case, I had a crystal with two nearly identical unit cell edges and all angles very close to 90&ndeg;, and it easily indexed as P4. It actually turned out to be P2 (which should have been obvious since P4 or even P222 would have been too small for the protein to fit!), but fortunately I had more than enough data anyway. Therefore, when Elves suggests P222, I often pick P2 if the crystal diffracts well enough that it won't be a problem to collect extra data.

On the other hand, Elves is also (deliberately?) pessimistic with regard to the very high symmetry space groups (such as I422 or P6), which it leaves out. You can still tell Elves to index with any space group you want, even if it's not listed, so if you're lucky enough to have a crystal with high symmetry and already know this, just enter the actual space group instead of one of the listed ones. Elves will go ahead and use whatever you tell it to as long as it's a recognized space group. In the most extreme case a wedge as small as 20 degrees will be enough. If you're trying to get experimental phases, or if you're just in a hurry, this is extremely helpful.
Elves will autoindex again (I'm not sure why), then print out a screen full of crystal info:

Wedger elves will create a script called mosflm.com (but will not run it.)
         and process from /data/mcfuser/ucb/alber/nat/lysozyme_0_001.img
                      to /data/mcfuser/ucb/alber/nat/lysozyme_0_001.img into raw.mtz
         using the orientation in auto.mat

        Data were collected from 88 to 89 degrees, in 1 degree steps with the 
        ALS 8.3.1 detector (gain = 1.8) at 450 mm from the crystal and
        the direct beam hit the detector at: 159.463 155.28

        X-rays were 1.0085 angstroms with polarization 0.9

        Unit Cell is 169.086 169.086 86.8517 90 90 120
        Spots will be measured out to 2.2 angstroms with space group P32
        and a mosaic spread of 0.710 degrees

        Postrefinement will be turned OFF.

        additional keywords:
        BACKSTOP RADIUS 2

           ^   ###  ####   #   ###    ##### #  # #  ###    ^
          /|\  #  # #     # #  #  #     #   #  # # #      /|\
           |   ###  ###  ##### #  #     #   #### #  ###    |
           |   # #  #    #   # #  #     #   #  # #     #   |
           |   #  # #### #   # ###      #   #  # # ####    |

      Make sure all the above numbers are correct.
          (Especially the beam center)

Do you want our opinion on your collection strategy? [Yes]
W. Elves-> resolution 3
When Elves asks me whether I want it to determine a collection strategy, I almost always first change the resolution cutoff by typing something like "resolution 1.9". The default is for the corner of the detector, which is probably not the real limit - I've already moved the detector so that the center edge is a little past the (guessed) maximum possible resolution. As far as I can tell this doesn't make a difference for the strategy, but (I think) it will change the calculated signal-to-noise ratio that Elves reports. This is very useful for collecting optimal SAD or MAD data.
Elves will then determine a collection strategy, based on what it determined about the crystal lattice and its orientation with regard to the beam. (FYI, the orientation of the reciprocal lattice changes along with the orientation of the crystal. This will be useful for other reasons that I'll describe on another page.)

strategizing ... (Ctrl-C to skip) 
This wedge will be 3.3% complete to 3.0 A and contain 0.0% of anomalous data.
A wedge from    4.0 to  94.0 degrees would be 100.0% complete.
A wedge from    4.0 to  94.0 degrees would contain 97.6% of anomalous pairs.
oscillation can be as much as 4.80 at phi = 44.0 224
             but no more than 0.70 at phi = 4.8 184.8
recommend: 
  start   osc frames  wedge  size
   -1.0  0.60    168  100.8 100.8

for details, see logs/strategy.log and logs/strategy.html

Update mosflm.com and exit Wedger Elves? [Yes]
W. Elves-> 
Hitting return will add a data collection run to the Blu-Ice GUI and set all of the recommended parameters for you (which you can change if you want; see below). Note: you may need to make changes to this when collecting SAD or especially MAD data; this is discussed below.

[edit]What the strategy means
===== Percent of anomalous pairs. ===== For MAD phasing, twice as many reflections are required in order to compare Friedel pairs. For instance, P2 will now require a full half of the reciprocal lattice to be sampled in order to have 100% complete anomalous pairs. A strategy that will give us complete native data is often (but not always) insufficient for complete anomalous data. Once again, tilting the crystal can help improve anomalous completeness. An inverse beam strategy (see below) is another possible solution.

If only native data are required (or if the only purpose of collecting anomalous data is to locate a metal site), the anomalous completeness can be ignored. Only the first completeness statistic matters.

===== Oscillation ===== This is not something you should ever change, unless you're especially paranoid and actually want to reduce it (the lowest possible is 0.1&ndeg;). Elves will never recommend an oscillation above 1&ndeg;, but depending on your crystal orientation, it may be much less. This is an excellent point to introduce one of the more obnoxious data collection problems:

====== Overlaps. ====== Sometimes Elves will print out this terrifying message when determining the strategy:

WARNING! with 1 degree oscillations you will have 3.9% overlaps when phi = 176
During each exposure, the crystal is rotated by the specified amount around the phi axis (i.e. the goniometer axis), which rotates multiple reciprocal lattice points through the surface of the Ewald sphere; the 2D projection of the intersection between lattice points and Ewald sphere is the diffraction pattern. However, for large unit cells the reciprocal lattice points in one or more directions will be very close together. A one-degree oscillation may rotate points on successive planes onto the same position on the Ewald sphere. As a result, multiple reflections will literally overlap on the diffraction pattern, making it impossible to accurately measure their intensities; these observations will be thrown out. Higher mosaicity will make this problem worse. James told me that overlaps are one of the most common reasons for failing to solve a structure. At the very least this can greatly reduce redundancy of observations (and mean I/sigma), and possibly result in incomplete data.

There are several ways to address this problem. If you're already aware that your crystals are problematic, you can try to freeze them in a particular orientation in the loop. But if you're already at the beamline and have steady hands, the crystal (or rather, the loop) can be very gently tilted so that the reciprocal lattice intersects differently with the Ewald sphere. A more general technique is to try for a particular orientation when freezing the problematic crystals. Alternately, smaller oscillations can be used so that formerly overlapping lattice points now occur on successive frames instead. Although "safer", this method again leads to increased collection and exposure time.

As a real-world example, I have crystals with a 135-Angstrom c edge that always have a flat plate morphology. These crystals tend to sit flat in the loop and on the beamline, the crystals will usually be shot with the beam exactly normal to the surface of the plate. This orientation leads to overlaps of up to 35% for some frames. The larger the unit cell, the worse the problem; the group studying the 30S ribosome subunit had to use 0.1 degree oscillations. The strategy provided by Elves may only require smaller oscillations for part of the range, and will include multiple wedges with different oscillation sizes. This will not be automatically sent to the graphical interface, and will need to be entered manually instead. Addendum: this used to be true, but I haven't seen it in a while so I'm not sure if Elves still does this.
The third way to deal with overlaps is to angle the detector instead of collecting with the beam near the center and the detector face normal to the beam. The parameter to change is "2theta" and is accessible through the "Hutch" tab in the BLU-ICE interface. A value of 20 degrees should be plenty. You need to take test shots again in this configuration. Re-index, making sure that Elves recognizes the change in 2theta; there should be a significant improvement in overlaps, and larger allowable oscillations. Depending on the space group, this may reduce completeness. Moving the detector back will also help with overlaps (and you will probably want to do this anyway when changing 2theta).

Finally, you can lower the beam divergence in the "Hutch" tab of Blu-Ice. I'm still unclear about exactly what this means, but it controls the width between slits that the beam passes through and has something to do with the angular divergence of the beam. In practice, the lower the divergence, the smaller the reciprocal lattice points (and the smaller the spots on the diffraction pattern), and thus the less likely they are to overlap.

===== Oscillation range ===== This is the start and end point of the wedge to collect. Elves will pad the required range on either side, so if you need 90&ndeg; of data to get 100% completeness, you'll probably get a strategy for approximately 100 frames. Don't fiddle with this. More importantly, you can't simply collect data from some random angle, unless you're collecting over a full 360&ndeg; - only the computer can tell what the orientation of the reciprocal lattice is, and the phi angle is meaningless except relative to the crystal orientation. (This also means that if you remove a crystal and put it back on later, the relationship between phi and the crystal will have changed again, so you need to reindex and recalculate a strategy.)

The number of frames you need varies by lattice, but this too is dependent on crystal orientation. Monoclinic lattices (P2 and C2) require 180&ndeg; around the reciprocal lattice, but sometimes a wedge much smaller than this can measure all of the reflections. Elves will tell you this too. I often collect extra data when my crystal diffracts well, either to ensure against picking the wrong lattice, or to increase redundancy and signal-to-noise ration to get higher-quality data. There is no drawback to doing this except for the potential for increased radiation damage or staying up too late babysitting your crystal. In some cases, e.g. SAD phasing with bromine (or worse, sulfur), extremely redundant data is a necessity; Christine collected 800&ndeg; to phase one of her structures with bromine SAD. James says that the quality of data is the same if you double the number of frames while cutting exposure time in half.
[edit]Figuring out the real lattice
For the ambiguous indexing solutions mentioned above, it will not be possible to distinguish between lattices until you actually process the images and scale in the higher symmetry spacegroup(s). If a P21 dataset is incorrectly processed as P212121 this will be immediately apparent from the high Rsym. Orthorhombic usually requires only 90 degrees due to higher symmetry (which translates to higher symmetry in the reflections), but in most cases this will not be sufficient for monoclinic lattices. You can determine the true lattice group very quickly: as soon as data collection starts, enter this on the command line:

   mcfuser@crush09 % cd ~/lab/user/project [e.g. ~/alber/nat/PknB/]
   mcfuser@crush09 % process
This will run Elves on the data being collected. If you make it to the scaling step before the run is complete, you should be able to tell for sure what lattice the crystal really is by looking at the Rsym. This will allow you to decide whether to collect more frames, or stop the run early once you have enough data. Pay attention to the completeness statistic at the end of integration (before scaling). However, do not stop ahead of time when you need to collect anomalous data, because 100% complete native data does not require that all Friedel pairs be measured.

[edit]Other parameters.
From the BLU-ICE interface, there are several other data collection options that may be extremely important:

==== Exposure time. ==== According to James, the point at which the average MAD data set starts to become unusable is only 300 seconds total exposure time. Depending on how strongly the crystal diffracts and what strategy Elves picked for it, the total exposure time may be much more than this. Unfortunately, the lower the exposure time, the worse the signal-to-noise ratio and the lower our chances of experimentally phasing the structure; resolution may be worse as well. This is even worse when the anomalous edge of interest is far from the peak flux, and is exacerbated by the worse radiation damage from heavy metals (especially at the peak). Elves now appears to provide some indication of what the signal-to-noise ratio will be and whether this is expected to be usable for phasing.

The only structure I've solved using SeMet MAD had a total of 100 seconds exposure time for peak on one part of the crystal and 200 seconds for inflection/remote on another part, all of these between 12000eV and 12600eV. Kristi told me she used even less time for PstP. Christine and I collected two successive runs of 400s at 13474eV on different parts of the same crystal for a successful bromine SAD dataset. (See also below.) This is very dependent on the type of atom and thus the exact wavelength used. My impression is that atoms with anomalous edges at shorter wavelengths (e.g. selenium, bromine, mercury) are going to be easier to deal with. See the next section for more detail.
For native data alone, much longer exposures are usually okay, since the 300-second line is where anomalous scatterers start to fry rather than applying to protein crystals overall. I still try to keep the exposure time to a minimum, especially if I don't know much about the crystals I'm working with. There is also usually a point at which the crystal just doesn't diffract any better with increased exposure time. A good strategy would be to collect twice as many frames as required at a reasonable exposure time, and then throw out any later frames that appear to have radiation damage. SAD data collection usually works something like this. James claims that collecting twice as many frames is equivalent to doubling the exposure time, and in some cases it may actually be better.

Different crystals have very different responses to radiation; small, poorly diffracting crystals often fry well before a complete dataset can be collected (e.g. when a 20s exposure is necessary to get a good image). James also told me that ultra-high resolution data is lost very quickly to radiation damage - but this isn't necessarily visible in the diffraction! So your 0.8A structure might not have any useful data beyond 1A. I haven't noticed any problems personally, but even in my highest-resolution structures I haven't been analyzing them closely enough to tell whether radiation is altering the structure.

One strategy I missed initially is to collect two identical wedges at short and long exposure times (in that order). For very well diffracting crystals this may be essential - the first wedge gets accurate low-resolution data without overloads (those yellow spots in the ADXV window), the second gets high-resolution reflections and better I/sigma values. For weakly diffracting crystals this strategy can be used to gather a complete and undamaged data set and then try for cleaner, higher-resolution data. If radiation damage is sustained on the second run the first wedge should still be enough to work with.
Note: James now has a method for determining when to stop collecting data for SeMet crystals based on the distinct shape of the fluorescence scan (see J Synchrotron Radiat. (2007) 14:51-72). This is much more rigorous than the 300-second rule, and he has a fairly easy protocol for taking the necessary readings.

==== Energy/Wavelength. ==== The default for 8.3.1 is 11111eV/1.115A, which is the point at which the flux is highest; other beamlines have their peak flux at different wavelengths. For native data, this is almost certainly sufficient unless you want ultra-high resolution.

===== Anomalous data ===== For anomalous data, whether for MAD or simply for obtaining an anomalous difference map, one or more wavelengths around the anomalous edge of our atom of interest is needed. That's another section entirely (see below). However, there may be reasons to collect anomalous data for purposes other than phasing - for instance, confirming the position and identity of metal ions that produce a significant anomalous signal. For some of my kinase crystals, I collected at both the default wavelength (to get high-resolution data) and the Mn peak @ 6542eV (which gave me huge anomalous difference map peaks).

For an anomalous difference map, you really need to collect data above and below the peak for the atom you're trying to locate, and generate maps for both. The data collected at a higher energy should have a much larger peak in the map if you've identified the atom correctly. Jaime and I tried to locate soaked Mn ions in FrzS crystals, but we didn't consider the presence of other relatively heavy atoms with significant anomalous signal at low energies, and we couldn't tell if the peak in the anomalous difference map was a manganese or a chlorine.
This probably doesn't matter to most people, but even at the default wavelength there is still a significant amount of anomalous signal for many atoms, including sulfurs in Met and Cys if they haven't already been fried, plus chlorine ions in solution, or any transition metals bound by the protein. If you don't actually know what the anomalous scatterer is but already know the position(s), you need to do an energy scan on beamline 12.3.1, which will cover a wide range of energies and positively identify the atom. This can work for atoms that are difficult or impossible to collect data at the edge, such as calcium (which Christine found this way in her protein).

==== Detector distance. ==== For my experiments, I usually only care about this to the extent that it determines the maximum possible resolution. My rule of thumb has always been that the signal-to-noise ratio should drop to 2 (James says 1.5) just before the edge of the detector; if spots occur in the corners these resolution shells will be incomplete. In my personal experience, the actual maximum resolution is often several tenths of an Angstrom beyond where I intially see spots; before I figured this out I often ended up missing a large amount of data. Zooming in on the edge of the image in the adxv window and typing 'h' to re-adjust the contrast may show where the spots actually end. However, higher redundancy can often boost the resolution by a significant margin.

Changing the wavelength will also change the maximum resolution possible for a given detector distance. Lowering the energy will lower the resolution and vice-versa. I don't know whether this is standard practice, but for MAD I use the same detector distance for every wavelength; the variation in resolution is not very large overall, and negligible between peak and inflection.

The minimum detector distance is 83mm, but if you've changed 2theta the detector needs to be further back. If you don't know what that means, ask for help - I nearly broke something the first time I tried this.

[edit]MAD/SAD data collection
There is now a separate page on MAD scans and wavelength selection.