---
title: Gmeigs Shutterless Data Collection Notes
layout: default
group: data_collection
---

Normal, monochromatic data collection:

Index and Strategize using "index" on the terminal command line.
Allow it to create a "run 1" for you.
Use the suggested starting angle, but change default to collect an entire 360 degrees of data.
Use the suggested shortest possible exposure time of 0.04 seconds (25 Hz).
Use the suggested oscillation angle, delta, which will be approximage 1/3 the mosaic spread.  
Be mindful of the "wedge" size, this defines the shutterless sweep size, 
make sure it is at least 360 degrees.
(DON"T FORGET to make a New Directory for this set of runs!)

By collecting at the shortest possible exposure time, 
you obtain a complete data set with minimal radiation damage.  
It's likely your crystal will still yield more good data by taking a "run 2" at a longer exposure time.

--->> NOTE:  Use 'exposure_time.com" to get an estimate of crystal life time and suggested exposure times.
Create a run #2 by clicking the Asterisk "*" under the "Run#" side-tab
Change the exposure time to be the max time given by "exposure_time.com" (minus 0.04 secs)
Go back to run 1 and press Collect to start data collection.

   $$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$$
      MAD MAD MAD     MAD MAD MAD     (SAD SAD SAD)    MAD MAD MAD    MAD MAD MAD

If you want to do MAD or SAD you are going to have to attenuate, because your crystal will die ~4 times sooner.
ALSO, the detector DOES have read out time of ~0.002 seconds,
This is NOT a problem for Native data but BAD for finding 1% differences in Friedel Mates:
You need to expose for LONGER times to keep this read out error to be LESS THAN 1%, i.e. for at least 0.2 Seconds.
This is the reason ATTENUATION is REQUIRED. 

Expected 1/2 life dose of typical protein crystals
Native    2e+7
MAD       5e+6
S SAD     3e+6
Br/I/RNA  1e+6
RT        2e+5

Moving monochromator to the absorption edge  of interest ( e.g. "wave.com Se") 
Attenuate the beam by lowering the divergence to 0.35 X 0.35, but no smaller than  0.25 X 0.25
Run "tuneup.com" at this Energy and Divergence
Press "update" in the collect TAB to read in current eV/Energy, or just enter it by hand.
Then take test shots AT THIS ENERGY! (~absorption edge?) 
Follow instructions for Index & Strategizing, BUT
Collect 180 degs (using the recommended starting angle) with "Inverse Beam" box checked!
Set WEDGE Size 30 or 45 Deg.!
(DON"T FORGET to make a New Directory for this set of runs!)
Take a fluorescence scan to find peak and inflection and remote.
Go back to RUN 1 in BLUICE and collect at 2 Energies (wave lengths) One energy "half way between Peak and the Inflection" 
  and  Another Energy at the "High Remote" ~ 200-400 eV above the {(peak + inflection)/2}
CLICK on the Asterisk to make more runs, up to 8 pairs of (peak+infl)/2 and remote wavelengths.
 