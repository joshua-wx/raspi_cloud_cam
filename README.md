Joshua Soderholm, Feb 2016
Climate Research Group, University of Queensland
Written for BSCH webcam network (Ben Quinn)

##Updates

11/4/14: Added htpupdate command to config file wget loop. Changed camera settings to default.
25/2/15: Updated raspistill setting to match Ben Quinns code

##Help

####Setup
Download Raspian “Wheezy” image from http://www.raspberrypi.org/downloads
Copy using correct method onto usb drive http://elinux.org/RPi_Easy_SD_Card_Setup
Ensure you expand the ext partition if the SD card is larger than 2GB, otherwise this space will be unavaliable.
plug in and connect power to pi
Default un: pi pass: Raspberry
Change timezone in raspi-config
reboot... enjoy!

#####Firmware Update
To update firmware install and run, then reboot
sudo apt-get install rpi-update

#####Install from repository
sudo apt-get update && sudo apt-get upgrade
sudo apt-get install zip msttcorefonts imagemagick curl ftp screen subversion libv4l-dev libjpeg8-dev

Compile htpdate from source ## NOW IN APT_GET REPO
The raspberry pi has no memory function for the onboard clock, therefore needs ntp to update the time. University and Government systems may block ntp protocols, an alternative using http time is htpdate...
installation:
Download C (tar file) source from link
unzip, make, sudo make install


####Setup webcam software
1. Copy bash scripts ~/webcam
2. Create the directory /tmp/mjpg_out
3. cd into directory from terminal and use sudo chmod 777 “file_name” for the webcam scripts so they can be executed.
4. Connect webcam via powered hub and ethernet/wifi
5. Run ./webcam_main
6. Comment htpupdate line is no http time control is required.

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


