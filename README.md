Joshua Soderholm, Sept 2017
Atmopsheric Obs Research Group, University of Queensland
Written for BSCH webcam network (Ben Quinn)

##Updates

11/4/14: Added htpupdate command to config file wget loop. Changed camera settings to default.
25/2/15: Updated raspistill setting to match Ben Quinns code
26/9/17: Tweaks to manual

##Help

####Setup
see albanyck_webcam_config


#####Install from repository
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install zip msttcorefonts imagemagick curl ftp screen subversion libv4l-dev libjpeg8-dev htpdate


####Setup webcam software
1. git clone repo
3. chomd 777 prod scripts and main script
4. Connect webcam via powered hub and ethernet/wifi
5. Run ./webcam_main

####Control webcam software
1. Run prob_local or prod_bsch to turn off/on the respective saving processes, status is advised.
2. Run prod_force_run to ignore stop start times in options file (run again to check)
3. User can set local save path (local_path), site name (site_name), bsch upload interval (bsch_interval), local save interval in miliseconds (capture_interval) and options download interval (options_interval) in the global vars list.
4. To terminate webcam program cleanly, delete the kill_script file in ./
5. To clean up after a forced crtl+c termination, run “killall mjpg_streamer” and “killall webcam_capture”

#####mount usb drive in terminal
check dmesg for dev path
sudo mount /dev/sda1 /media/WEBCAM_HDD


#####Convert jpg images to timelapse
sudo apt-get install mencoder
cd to directory with target jpg’s in
ffmpeg -r 24 -pattern_type glob -i '*.JPG' -c:v libx264 output.mpeg


