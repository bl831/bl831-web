---
title: Pilatus Data Collection
layout: default
group: data_collection
---

<nav aria-label="breadcrumb">
  <ol class="breadcrumb">
    <li class="breadcrumb-item"><a href="/procedures/data_collection/data-collection/">Data Collection</a></li>
    <li class="breadcrumb-item active" aria-current="page">{{ page.title }}</li>
  </ol>
</nav>

---

# Notes on Pilatus Data Collection

---
***Notes collected by MCT in 2016 following installation of Pilatus at 8.3.1***

These notes on (cryo) data collection with the Pilatus are based on a conversation with James Holton on July 27, 2016:

* For native CRYO data:
	* Collect data so that the crystal is exposed for 1 second per degree of rotation. A data set that consists of a 360 degree pass should take 360 sec. (6min)
	* This means your oscillation (per image) should be equal to your exposure time in seconds.
	* The oscillation per image should be no more than 1/3 of the mosaic spread of your crystal, and the recommended strategy is to collect data at 20Hz, which means 0.05 degree oscillations and 0.05 sec. exposures. (Data sets will be very large.)
	* Collect a full 360 degrees, since it will be fast anyway, and weaker signal due to short exposure times will be compensated for by higher redundancy.
		* At 0% attenuation and standard divergence (11111keV), Holton reports that a crystal will last for no more than 258 sec. (4.3 min), so if you collect 360 degrees at 1 sec. exposure per degree, the end of your data set may suffer from radiation damage and you will probably have to cut some of the later frames (decide where to cut using Rdiff from XDSSTAT).
			* This is ok for SG with reasonable symmetry, but you may have to rethink this if you are stuck with very low symmetry (i.e. P1).
	* These notes apply to collecting native data... I assume that one would want a different (inverse beam?) strategy for collecting anomalous data. If you want to do an anomalous experiment, I recommend talking to Holton about it and looking at the resources on the BL8.3.1 website: http://bl831.als.lbl.gov/~gmeigs/data_collection/index.html

A different, more traditional strategy is needed for ROOM TEMP data, because the tolerable dose limit is much lower. RT data collection may require some optimization, but the following could be a good starting point (I have collected some really good CypA datasets using this protocol):
* Beam Divergence: 1.0 x 0.35
* Attenuation: 80% or 70%
* Oscillation: 0.5 degrees
* Exposure Time: 0.2 sec.
* Collect as much data as possible before obvious decay, and retrospectively cut the data when damage becomes too severe. (Decide where to cut using Rdiff from XDSSTAT.)