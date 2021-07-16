---
title: ALS 8.3.1 Cheat Sheet
layout: default
group: data_collection
---

# ALS 8.3.1 Room Temperature Cheat Sheet

---

<div class="alert alert-warning d-flex align-items-center" role="alert">
  <i class="bi bi-info-circle-fill px-2" style="font-size: xx-large; color: blue"></i>

  <div>
    make sure that all data is being written within the /data directory and that all data processing is being performed in the “/home” directory.
  </div>
</div>

Have one terminal open for `/data` and one open for `/home`.  

For other questions: http://bl831.als.lbl.gov/

To open terminal right click the mouse, go to open trerminal

The computers should be pre-configured for data collection, but if not, open a terminal window and type `go`

1. Find fraser in the `/data` directory. Create a new directory for yourself in

   ```bash
    /data/mcfuser/ucsf/fraser/your_directory/your_directory_for_today
   ```

2. In the other terminal window find fraser in the `/home` directory. In this directory make a
   directory for yourself. Issue your future commands from here.

   ```bash
    /home/mcfuser/ucsf/fraser/your_directory
   ```

3. Change the cryojet temperature to 273K using UNIX command line (`cryojet.com 273K)` /home
4. Move cryojet back using cryojet.com move out
5. Move crystal pin back to allow extra space for capillary using UNIX command line (pinlength.com 29.5) /home
6. In the BLU-ICE window where it says "Directory", type in the folder-name that you created in the /data directory. Use BLU-ICE program to collect two test shots at 90o to each other. You should be in tab 0 of BLU-ICE.  [Folder-name = /data/mcfuser/ucsf/fraser/yourfolder/yourfolderfortoday]

**Each time you take a test shot the image will be saved in this folder-name directory. When collecting a data set make sure to create a new directory so that it is separate from the test shots, more on that below.

Prefix is where you can give a specific name like "LK001", but this is unnecessary for test shots.  

   a.  NOTE: always do single “test shots” in BLU-ICE collection window 0
   b.  NOTE: make sure Aluminum filter is in use, this is in the tab called Hutch. - this is only for room temperature data - you can also achieve similar attenuation by setting beam divergence to 0.3x0.35 (also in the hutch) 


7. If you like what you see follow these steps to collect a data set.
8. Index the two test shots and determine a data collection strategy using Elves (type "index", MAKE SURE THIS IS DONE IN THE /home DIRECTORY)

    a. Hit “return” to get through the prompts until program asks to “Update mosflm.com and exit Wedger Elves?”.  Hitting return again will update BLU-ICE GUI with the new collection strategy.

9. Next you will run waypoint. On the push screen select a position where you want the translation to end, then in the command line in the /home directory type, "waypoint.tcl". Then on the push screen press where you want translation to begin.
10. Before pressing Collect on BLU-ICE you want to make sure you have updated where the data will go.  

Go to the /data directory and create a new directory, like the one below:

    /data/mcfuser/ucsf/fraser/your_directory/your_directory_for_today/LK001

In tab 1 in BLU-ICE update the Directory line to collect data into the directory you have just created. 
Press Collect in tab 1 on BLU-ICE
After the data set is complete press Control (ctrl) C to exit the program on the /home directory.
Repeat this process every time you collect a new data set. 

13.     Manually reset the cryojet position (return cryojet position such that it is touching the outer circle of the hash marks).
14.     Reset the crystal pin length before leaving (pinlength 18) /home.

11.     At least 30 min before leaving, after you're done collecting data, one types "finish" or "finished" in a terminal window that will turn OFF the cryojet HEATER and allow it to reach its minimum temperature. This can also be accomplished by typing "cryojet.com on", but NOT this (e.g): "cryojet.com 100K", this will leave the heater ON.

12. Reset cryostream temperature to 100K (cryojet.com 100K) /home.


Unix Cheat Sheet for commands needed at the beamline:

pwd- print working directory. Shows you where you are in the directories.
ls- lists everything within a directory.
cd- change directory. But you must indicate where you are going, for example "cd Documents" will take you to the Document directory.
mkdir- make directory. Will make a directory within the directory you are in. For example within the fraser directory to make a directory called lillian, I would type "mkdir lillian"
cd ..- takes you up a level in the directories. So from the lillian directory I would type "cd .." And then be in the fraser directory.



When you get back home  (this will need much much more work):
SSH into the server at the beamline. Directions on how to do this is on the Transferring Data from the ALS page. Copy your data onto the computer in the lab. Within the directory that you would like to process data from make a new directory called "xia2". change into the xia2 folder "cd xia2" Run "xia2-3dii ../" To begin data reduction, see the following pages: Xia2 Data Processing,xia2 notes,xia2 manual