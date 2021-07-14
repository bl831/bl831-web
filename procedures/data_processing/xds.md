---
title: XDS Data Processing
layout: default
group: data_processing
---

# Processing data with XDS at 8.3.1

---

<div><i><font face="verdana, sans-serif">From Holton on Dec. 14, 2016, re: processing fresh data while at ALS 8.3.1:</font></i></div>
<div><font face="verdana, sans-serif"><br>
</font></div>
<div><font face="verdana, sans-serif">It's not exactly ready for prime time, but it's called <b><i>xds_rollup.com</i></b>.</font></div>
<div><font face="verdana, sans-serif">You point it at one or more root directories and it runs xds_runme.com</font></div>
<div><font face="verdana, sans-serif">on each. &nbsp;The result can be a bit of a mess, with different space groups</font></div>
<div><font face="verdana, sans-serif">and sub-groups represented, different indexing conventions etc all over,</font></div>
<div><font face="verdana, sans-serif">but at least the processing is organized into chronologically ordered</font></div>
<div><font face="verdana, sans-serif">"wedge" directories under the directory where you launch it. &nbsp;It is</font></div>
<div><font face="verdana, sans-serif">designed to run over-and-over again, adding wedges as you go. &nbsp;It will</font></div>
<div><font face="verdana, sans-serif">also try to re-run every wedge in P1 (for reference) and also use DIALS.</font></div>
<div><font face="verdana, sans-serif"><br>
</font></div>
<div><font face="verdana, sans-serif">Cleaning up the mess is still more of a work in progress.</font></div>
<div><font face="verdana, sans-serif"><b><i>~jamesh/Develop/xds_followup_notes.com</i></b> is an attempt to try to&nbsp;</font></div>
<div><font face="verdana, sans-serif"><span style="font-size:13.3333px;background-color:transparent">clean up&nbsp;</span>the mess. &nbsp;Every possible re-indexing operator between every pair&nbsp;</font></div>
<div><font face="verdana, sans-serif"><span style="font-size:13.3333px;background-color:transparent">of&nbsp;</span>wedges is enumerated, applied, and an R-factor calculated. &nbsp;The</font></div>
<div><font face="verdana, sans-serif">minimum-R connections can then be grouped into clusters, and re-indexed</font></div>
<div><font face="verdana, sans-serif">into potentially compatible merging groups. &nbsp;It takes a very very long</font></div>
<div><font face="verdana, sans-serif">time, proportional to the square of the number of data sets. &nbsp;But it is</font></div>
<div><font face="verdana, sans-serif">the only general solution to the problem.</font></div>
<div><font face="verdana, sans-serif"><br>
</font></div>
<div><font face="verdana, sans-serif"><br>
</font></div>
<div>

<div><font face="verdana, sans-serif"><i>Practically speaking:
</i></font></div>
<div><font face="verdana, sans-serif"><br>
</font></div>
<div><font face="verdana, sans-serif">From "control computer" ("graphics3"?) at 8.3.1:</font></div>
<div>
<ul><li>ssh dataserver4</li>
<li>cd /home/mcfuser/ucsf/yourusername/ddMMMyyyy/</li>
<li>mkdir <a href="http://xds_rollup.com" style="font-family:verdana,sans-serif;background-color:transparent;font-size:10pt">xds_rollup.com</a></li>
<li>cd&nbsp;<a href="http://xds_rollup.com/" style="font-family:verdana,sans-serif;background-color:transparent;font-size:13.3333px">xds_rollup.com</a></li>
<li><a href="http://xds_rollup.com" style="font-family:verdana,sans-serif;background-color:transparent;font-size:10pt">xds_rollup.com</a><span style="font-family:verdana,sans-serif;background-color:transparent;font-size:10pt">&nbsp;/data/mcfuser/ucsf/keedy/ddMMMyyyy/</span></li>
<li>Will continue forever. &nbsp;Can kill whenever, then restart later (presumably in same way, but when logged in remotely).&nbsp;</li></ul>
</div>
</div>
<div><br>
</div>
