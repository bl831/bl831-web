---
title: RT Data Collection
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

# How to Do: RT Collection Notes

---

<div>
<p><b>When you are done with your data collection</b></p>
<ul><li><b>turn cryostream back on (NOTE: This takes at LEAST 30 minutes. Don't screw over the next shift!!!!) - &gt; cryojet.com on</b></li>
<li><b>move cryojet back into position so that the end is touching the sample centering circle on the TV</b></li>
<li><b>type "finished"</b></li></ul>
</div>
<div><br>
</div>
USING MICRORTs:
<div>vary humidity by adding variable amounts of mother liquor and H2O. &nbsp;I usually start with 8ul Mother Liquor and 2ul H2O, but will often go to 50/50. &nbsp;Using a long thin p10 (get from xtal room before leaving, Krogan and Kortemme ones are too wide), pipette these things as far down the MicroRT as you can. &nbsp;Then add to a a microtube and spin down. &nbsp;If the pinlength is back to 29.5 and the cryojet is all the way back, you should be good to add it without cutting the tube.</div>
<div><br>
</div>
<div>Data collection:<br>
I wrote a little jiffy program for doing what some call "vector scans" where the crystal is translated during data collection.  It is called "waypoint.tcl".  What you do is center the crystal on the place where you want the data collection to end, launch "waypoint.tcl" from the command line, then center the crystal on the place where you want the data collection to start, and then  push "Collect".  The distance between these two points will be divided evenly into as many steps as you have images in your data set, and the crystal will be translated automatically after each shot.<br>
<br>
<p>Set up for experiment
</p>
<ul><li>turn off cryostream
</li></ul>
<p>&gt;cryojet.com off <br>
</p>
<p>or</p>
<p>&gt;cryojet.com 273K<br>
</p>
<ul><li>move pin back to allow for capillary
</li></ul>
<p>&gt;pinlength.com 29.5</p>
<p>Can also adjust cryojet position by dialing the front nob.&nbsp; After, you must return cryojet position such that it is touching the outer circle of the hash marks.<br>
</p>
<p>Reset BLU-ICE parameters 
The procedure was developed almost entirely by James Holton:
</p>
<ul><li>Beam divergence -&gt; 0.5 horizontal
</li>
<li>Aluminum foil (added copper for low res pass)
</li>
<li>energy was at 13,000 eV 
</li></ul>
<p><b>An alternative approach to adding aluminum foil for attenuation ... can set beam divergence to 0.3x0.35 and leave foils out.</b></p>
<p>always run tuneup.com after changing settings
</p>
<p>shoot time was: 
</p>
<ul><li>high res shots were 15 sec exposures
</li>
<li>low was 1 sec 
</li>
<li>mid was 5 sec.
</li></ul>
<p>if your crystal is dying
</p>
<ul><li>raster along the crystal
</li>
<li>try changing energy (eg 12000 eV)
</li></ul>
<p>&gt;cryojet.com on</p>
<ul><li>reset pin length
</li></ul>
<p>&gt;pinlegth 18
</p>
</div>
