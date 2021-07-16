---
title: Remote Access
layout: default
group: remote_procedures
---

# Remote Procedures

---

Whether you are operating the sample mounting robot manually and collecting data ineteractively or
using the beamline for fully automatic unattended screening you will access the Blu-Ice control
software from a linux desktop using a NoMachine NX client.

## Connect to beamline using NoMachine NX

1. Make sure you have the latest version of NoMachine's
   [NX Client](https://www.nomachine.com/download)  

2. Configure your connection profile thusly:
   Set `Name` to something you will recognize (BL831 in this example), and set the `Host` to
   bl831.als.lbl.gov `Port` to 4000, and `Protocol` to NX. <img src="/assets/images/nx_setup_1.png" class= "img-fluid rounded-3 py-3" alt="Image of NX Connection Profile 1" >

3. Check the `Use password authentication` option. The rest of the setting can probably be left as-is. <img src="/assets/images/nx_setup_2.png" class= "img-fluid rounded-3 py-3" alt="Image of NX Connection Profile 2" >

4. Request a login.

5. Connect to the gateway using NX, and create a new session (for first time you connect) or select
   existing session if one already exists.

6. Open a terminal window and launch Blu-Ice by typing `go`.

7. I'm sure there are more details we could add, but hopefully it's fairly self explanatory. Just
   [contact us](/contact/) if you have any problems getting connected or configuring a remote desktop session.

## Load sample list using crystal-server webapp

If you will use the screening or unattended data collection features of Blu-Ice you will be required
to upload a list of your crystals as an Excel spreadsheet. You can download a template Excel file,
fill out the details, and then uplaod your filled out spreadsheets to the
[Crystal Server](https://bl831.als.lbl.gov/crystal-server).

Again, it should be self explanatory. Please [contact us](/contact/) us if you run into problems.
