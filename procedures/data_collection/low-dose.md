---
title: Low Dose Data Collection
layout: default
group: data_collection
---

# Ultra-Low Dose Data Collection & Processing
---
Protocol developed by Mike Thompson, with much guidance from James Holton. It is still in progress - suggestions welcomed.
<div><br>
</div>
<div><b>This protocol was developed to facilitate data collection at room temp, but can be applied to any case where minimization of X-ray dose and radiation damage are important.</b> Additionally, it works best for long rod-shaped crystals, because several datasets can be collected from a single crystal by translating the crystal to bring fresh material into the beam. If your crystals are small in all three dimensions, this general strategy will still work, but will require much more (or much more clever) crystal mounting. My favorite untested idea for doing this with crystals that are small in all three dimensions is to somehow get them lined up in a kapton tube by either sucking them up or just growing them directly in the tubes.</div>
<div><br>
</div>
<div><b>The general idea is summarized in this slide:</b></div>
<div><b><br>
</b></div>
<div><br>
</div>
<div>
<div style="display:block;text-align:center;margin-right:auto;margin-left:auto"><a href="https://sites.google.com/a/fraserlab.com/ucsf-private/protocols/crystallography/data-movement-processing-and-refinement/ultra-low-dose-data-collection-processing/low_dose.jpg?attredirects=0" imageanchor="1"><img border="0" height="225" src="https://sites.google.com/a/fraserlab.com/ucsf-private/protocols/crystallography/data-movement-processing-and-refinement/ultra-low-dose-data-collection-processing/low_dose.jpg" width="400"></a></div>
<div style="display:block;text-align:center;margin-right:auto;margin-left:auto"><br>
</div>
<br>
</div>
<div><br>
</div>
<div><b>Key steps for data collection, assuming you have rod-shaped crystals:</b></div>
<div><br>
</div>
<div>
<ol><li><span style="font-size:13.3333px">Prepare the beamline for RT data collection as normal, by retracting the cryojet and setting the temperature with cryojet.com</span></li>
<li>Mount your crystal in a loop. For applying this strategy to rod-shaped crystals, I prefer to use MicroLoopsE from Mitegen. Either the "vertical" or "inclined" versions of these loops are good, because you want the long dimension of your crystal to be almost, but not quite, parallel to the goniometer rotation axis (phi). Seal the crystal with a MicroRT tubing and grease. Make sure there is a small plug of mother liquor in the tubing to prevent dehydration.</li>
<li><span style="font-size:13.3333px">Use pinhole.com to choose the smallest pinhole that allows your crystal to remain bathed in the beam as it is rotated a full 360 degrees.</span></li>
<li><span style="font-size:13.3333px">Use tuneup.com to optimize the beam and, measure the flux. Record the flux in both photons/s and Gy/s - this is important (see below, and Appendix 1).</span></li>
<li><span style="font-size:13.3333px">Adjust the beam divergence to achieve the desired dose rate (Gy/s):</span></li>
<ul><li><span style="font-size:13.3333px">The optimal total dose per 180 degrees of rotation is 12-20kGy.&nbsp;</span></li>
<li><span style="font-size:13.3333px">I typically use 0.5 degree oscillations, so the dose per image should be 33-55Gy.&nbsp;</span></li>
<li><span style="font-size:13.3333px">I generally collect 0.04 (40ms) exposures, so the 360 images needed for a 180 degree wedge are collected in 14.4s.</span></li>
<li><span style="font-size:13.3333px">To deliver 12-20kGy in 14.4s, the dose rate needs to be 833-1390Gy/s</span></li>
<li><span style="font-size:13.3333px">Reduce the flux to be 833-1390Gy/s by changing the beam divergence. The default divergence settings are 2.0mrad horizontal and 0.35mrad vertical, which is what the slits should have been set at when the flux measurement was performed by tuneup.com (see above). The flux scales approximately linearly with the divergence slit width. So for example, if you change the divergence from 2.0x0.35 to 0.2x0.1, the flux would then be what you measured originally, multiplied by two ratios describing the reduction in divergence (i.e. flux*(0.2/2.0)*(0.1/0.35)). It is probably not advisable to set the divergence below 0.1x0.1. If you need to reduce the flux by more than a factor of 0.014, you can do so by also inserting the Al foil (if you do this, be sure to measure the flux at default divergence settings with the foil in place).</span></li></ul>
<li>Organize the data collection so that all the image files generated from a single crystal are output to the same directory, and create a separate run (BluIce tab) for each unique position along the crystal from which data are collected.</li>
<li>Start at one end of the crystal, and collect 2-3 high dose images that can be used to bootstrap the indexing of the low dose data. Use 2-3s exposure time for this, and separate 2 images by 90 degrees for optimal results. Index these images with elves or the autoXDS run (assuming you're at 8.3.1, if not most beamlines should have some tool to quickly index from a few snapshots). Record the space group (or at least the lattice type) and cell dimensions.</li>
<li>Translate the crystal and center the beam on a fresh, unexposed region. Ensure that the edge of the new beam position is at least 10um from the edge of the old position.</li>
<li>Low dose data sets should be 1440 frames, with 0.5 degree oscillations, and 0.04 (40ms) exposure time. This gives 720 degrees of data. You may decide you want to cut these wedges to be shorter, but it is best to collect too much data and exclude some during data reduction if there is any evidence of damage. Note: you might not see more than one or two occasional low-res spots on the detector. If your crystal diffracted well for the high dose images, it's diffracting for the low dose images too - you just can't see it.</li>
<li>Collect as many datasets as possible by repeating steps 8-9 until you run out of crystal.</li>
<li>Mount a new crystal, and again repeat steps 8-9 across the entire crystal. You don't have to repeat step 7 for each crystal if they are the same crystal form.</li>
<li>Collect at least 15 datasets using this strategy, but more is always better. As many as 25-30 or more is not unreasonable.&nbsp;</li>
</ol>
<div><br>
</div>
<div>
<div><b>Data Processing:</b></div>
</div>
<div><b><br>
</b></div>
<div>All of the data processing is done using various pipelines in Xia2. The general workflow is as follows: Rough indexing, followed by outlier removal based on unit cell isomorphism, then careful integration and "supermerging" of many datasets.</div>
</div>
<div><br>
</div>
<div>*NOTE: a lot of this could be scripted up to save time, but I haven't gotten around to it yet.</div>
<div>
<ol><li><span style="font-size:13.3333px">For each dataset in a crystal directory ( /crystal/ ), make a corresponding subdirectory ( /crystal/run1 , /crystal/run2 ... )</span></li>
<li><span style="font-size:13.3333px">Navigate into one of the "runN" directories and run Xia2 for the corresponding data set:</span></li>
<ul><li>The goal of this first run is just to get accurate unit cell parameters for each data set.&nbsp;</li>
<li>Run Xia2 using: 'xia2 pipeline=3dii image=../image_prefix_N_00001.cbf:1:180 unit_cell=a,b,c,alpha,beta,gamma space_group=sg'</li>
<ul><li>In this example command above:</li>
<ul><li>Xia2 is using XDS/XSCALE, utilizing all reflections from images 1-180. This is the first 90 degrees of your wedge, and it should be sufficient for accurately measuring and determining the cell parameters.</li>
<li>N = the run number</li>
<li>'a,b,c,alpha,beta,gamma' as well as 'sg' should come from the quick indexing you did with the high dose images</li></ul></ul></ul>
<li>Repeat step 2 for each data set that you would consider merging together, and record the output unit cell axis lengths and angles for each.</li>
<li>Decide which of the datasets can actually be merged together, based on isomorphism considerations.&nbsp;</li>
<ul><li>Currently, I'm just choosing the largest possible group of datasets whose unit cell axis lengths and angles don't differ by more than 0.2-0.3%.</li>
<ul><li>This is admittedly a pretty arbitrary way of selecting the optimal group of datasets to merge, and not the best way to do this. Should replace this step with something much more quantitative, such as clustering or iterative removal of datasets with recalculation of stats.&nbsp;</li></ul></ul>
<li><span style="font-size:13.3333px">Create a new subdirectory for your "supermerge" and navigate into that directory.</span></li>
<li><span style="font-size:13.3333px">Now perform the "production run" of Xia2 to produce your final MTZ. Your command will look like this:</span></li>
</ol>
<div><br>
</div>
</div>
<div>
<div><span style="font-size:13.3333px">xia2 pipeline=dials \</span></div>
<div><span style="font-size:13.3333px">space_group=sg unit_cell=a,b,c,alpha,beta,gamma \</span></div>
<div><span style="font-size:13.3333px">multiprocessing.mode=parallel multiprocessing.njob=2 multiprocessing.nproc=3 failover=True trust_beam_centre=True read_all_image_headers=False \&nbsp;</span></div>
<div><span style="font-size:13.3333px">image=/full/path/to/raw/images/image_prefix_1_00001.cbf \</span></div>
<div>
<div>image=/full/path/to/raw/images/image_prefix_2_00001.cbf \</div>
</div>
<div>
<div>image=/full/path/to/raw/images/image_prefix_3_00001.cbf \</div>
</div>
<div>
<div>image=/full/path/to/raw/images2/image_prefix2_1_00001.cbf \</div>
</div>
<div>
<div>image=/full/path/to/raw/images2/image_prefix2_2_00001.cbf \</div>
</div>
<div><span style="font-size:13.3333px">d_min=1.6</span></div>
</div>
<div><span style="font-size:13.3333px"><br>
</span></div>
<div>
<ul>
<ul><li><span style="font-size:13.3333px">Notes on the above example command:</span></li>
<ul><li><span style="font-size:13.3333px">At this point, switch from XDS (pipeline=3dii) to DIALS (pipeline=dials) because DIALS is better at integrating very weak spots.</span></li>
<li><span style="font-size:13.3333px">Once again, use 'sg' and 'a,b,c,alpha,beta,gamma' from your initial high dose indexing.</span></li>
<li><span style="font-size:13.3333px">In the short example, there are only 5 datasets - one crystal has 3 datasets, another has 2 - but your real command will likely have many more "image=" lines, since there is one per data set.</span></li>
<li><span style="font-size:13.3333px">As written above, this will process the entire wedge you collected, which was 720 degrees (1440 images with 0.5 degree oscillations)&nbsp;and 48-80kGy total dose. You may want to cut this down. To use, for example, only the first 360 images (180 degrees) from each dataset, add ':1:360' to the end of each line specifying image inputs (e.g.&nbsp;</span>image=/full/path/to/raw/images/image_prefix_1_00001.cbf:1:360).</li></ul></ul></ul>
<ul>
<ul><li>Notes on choosing a resolution cutoff:</li>
<ul><li>Generally, I will repeat step 6 several times to find the optimal resolution cutoff. I begin with something that I know is a bit overly ambitious, based on the high dose images. For example, if your high dose images show visible Bragg peaks out to 1.8A, do your first iteration of step 6 with d_min=1.6.&nbsp;</li>
<li>After your first run of Xia2 with DIALS, use the tables from the file 'working/directory/for/xia2/LogFiles/AUTOMATIC_DEFAULT_aimless.log' to choose a more optimal resolution cutoff. (Search the Aimless log file for '$TABLE')</li>
<li>Note that because of the very high multiplicity, you will need to consider carefully which merging statistics are most useful for guiding your resolution cutoff. I've found that CC1/2 is probably the best indicator of resolution cutoff for these very high multiplicity data sets. A CC1/2 of 0.3-0.4 in the high res bin seems reasonable to me. You also want to make sure your high-res measurements have high multiplicity (50 is probably about the minimum, but 100-150 or more is best). Finally, it seems to me (based on my limited experience) that it is acceptable to have low I/sig(I) for these data sets (as low as 0.3-0.5 in the high res bin), owing to the very low dose.&nbsp;</li>
<li>Repeat step 6 using the new d_min you selected based on the aimless log. (Note that in order to repeat your Xia2 run with a different d_min, you will need to delete (or move) all of the Xia2 output from any previous run so it is no longer present in the working directory. Evaluate the final statistics in the Xia2 output. It's probably not necessary to dig into the Aimless output at this point.&nbsp;</li>
<li>You may have to repeat step 6 a few more times to tune the d_min to the exact optimum.</li></ul></ul></ul>
<ul><li>The final output MTZ file will be <span style="background-color:transparent;font-size:10pt">'working/directory/for/xia2/DataFiles/AUTOMATIC_DEFAULT_free.mtz'&nbsp;</span></li>
<li><span style="background-color:transparent;font-size:10pt">The final data reduction statistics will be in&nbsp;</span>'working/directory/for/xia2/xia2.txt'</li>
<li>You may want to reassign R-free flags using the phenix reflection file editor (if you want to copy them from another MTZ file, or add them in a more controlled way).</li></ul>
<span style="background-color:transparent;font-size:10pt">&nbsp;</span></div>
<div><b>Appendix 1</b></div>
<div><br>
</div>
<div>How to calculate dose rate (Gy/s) from photon flux (photons/s):</div>
<div>
<ul><li>dose rate (Gy/s) = flux / (k_dose*Lh*Lv), where k_dose = (2000/(lambda)^2), Lh = horizontal beam dimension, Lv = vertical beam dimension</li></ul>
<ul><li>The above equation is a rearrangement of Equation 5 in James Holton's paper: https://journals.iucr.org/s/issues/2009/02/00/xh5015/xh5015.pdf</li></ul>
<div><b><br>
</b></div>
<div><b>Appendix 2</b></div>
</div>
<div><br>
</div>
<div>Another very accurate way to measure the dose:</div>
<div>
<ul><li><span style="font-size:13.3333px">Run "diode.com move in"</span></li>
<li><span style="font-size:13.3333px">Manually open the shutter. Tab is at the bottom right of BluIce GUI window.&nbsp;</span></li>
<li><span style="font-size:13.3333px">Run "flux.com"</span></li>
<li>Record flux in your notes.</li>
<li>Run "diode.com move out"</li></ul>
</div>
