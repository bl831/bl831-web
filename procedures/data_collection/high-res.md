---
title: High Resolution Data Collection
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

# Some Notes On Collecting Very High-Resolution Data

---

Jaime, Ho, Mark, and I have done this for specific projects where true atomic resolution (approaching 1 angstom) was the goal, but occasionally someone gets lucky and accidentally obtains a perfect crystal which diffracts beyond the range of the detector at the normal wavelength. This isn't actually a very difficult "problem" to solve - just a few changes to the normal routine are necessary.

---

## Screening

This procedure is what I've found useful in the past; try these steps in the order listed:

### Determine maximum resolution

Move to the very corner of the image in ADXV and press 'h'. If you can still see distinct spots, the resolution limit is at least this far. If not, move to the midpoint of an edge of the image, press 'h' again, and look for spots. If they don't reach this far, the detector is too far in or the wavelength is too high. Otherwise, your resolution is somewhere in between. Repeat this step each time you change something (unless the detector is tilted).

You can also try increasing exposure time to see what effect this has on resolution. I find there are diminishing returns from longer exposures - in fact, crystals that go to atomic resolution will usually still diffract well beyond 2 angstroms at 0.1s, the shortest exposure time possible. **Remember, high resolution features will be fried first** (sulfurs too), so don't get greedy - you may be much better off with 1.2A data @ 2s exposures than 1.1A data @ 10s exposures (especially if you're not actually *trying* to get high resolution in the first place).

### Move the detector in

At 8.3.1, the minimum distance is 85mm. You can collect complete data out to approximately 1.2A (? check this) at the default energy of 11111eV (1.116eV); the resolution at the corners of the detector is much higher.

If the detector is all the way in and spots are still off the edge, either or both of the next two options are required:

### Increase the energy

Or more appropriately, decrease the wavelength, which according to Bragg's law will reduce the scattering angle of each reflection. I start with around 13000eV, which is far enough to make a significant difference while retaining about 2/3 the maximum flux. I've never gone past 15000eV; the beam is just too weak.

### Increase 2theta

This is the angle at which the detector is tilted. Except for special cases, this will always be zero for "normal" crystals. Tilting the detector will capture reflectings at larger scattering angles (the maximum scattering angle that can be captured with the Q315 detector horizontal at a distance of 127mm is 61.65 degrees). **Move the detector back to 100mm first!** Next, click on the "Hutch" tab in Blu-Ice and change the 2theta menu to 20 degrees, then press "Start." Once this is done, go back to the "Collect" tab and take another couple of snapshots. The images will look weird but the processing software will have no problem interpreting them as long as it knows about 2theta (this should be automatic). Now the top edge of the image is much further out. If you don't see spots all the way to the edge, you can lower 2theta or the photon energy.

These techniques are complementary, and it's not uncommon to need to use both. As the spots get closer and closer together, you're much more likely to get overlaps (depending on symmetry). 2theta can help prevent this, which is why we sometimes use it for non-atomic-resolution data collection. However, with 2theta increased, it may potentially be more difficult to collect complete data (although I don't think I've had this problem yet).

From George: You may have problems with spot separation in the low-to-middle resolution range at close detector distances and/or higher energies. One way to tell is if when you index, it suggests very small oscillations (like around 0.2 or less), the implication is there is only a very small range in which you can collect reliable data because of overlapping spots.

For a sub-atomic resolution (~0.8 angstroms) crystal, the parameters could easily be 100mm detector distance, 2theta = 20 degrees, and energy = 15000eV. In the most extreme cases I've seen, even this was not enough to keep spots from spilling over the top edge of the detector. Fortunately, these proteins weren't interesting enough for me to waste time with even higher energies and longer exposure times. You can of course raise 2theta above 20, but this makes me uneasy, and it will complicate your data collection strategy.

---

## Data collection

==== Indexing ==== Do this the normal way, using two images (90 degrees apart) taken at the appropriate 2theta and wavelength. Hopefully this will not present any problems and will provide a clear strategy. You may have completeness problems if 2theta is high; alternately, you might need oscillations smaller than 1 degree depending on the unit cell size and crystal orientation.</p>

More here soon.
