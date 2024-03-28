# Bionic Modulation uses multiples Modulation with Hackrf and bionic (ubuntu 18.04) as : FM Modulation, BPSK, DBPSK,
# INSTALLING LXD
## For recent version by snap
```  
apt update
```  
```  
apt install snapd 
```  
```  
snap install lxd 
```  
```  
snap install lxd-client
```  
```  
sudo usermod -a G lxd $USER  
```  
```  
export PATH=$PATH:/usr/local/bin  
```  
## For old version by only apt
```  
apt update
```  
```  
apt-get install lxd 
```  
```  
apt-get install lxd-client
```  
```  
sudo usermod -a G lxd $USER  
```  
```  
export PATH=$PATH:/usr/local/bin  
```  
# GETTING BIONIC OS 
```  
lxc launch ubuntu:18.04 BionicModulation
```
```  
lxc exec BionicModulation -- bash
```
If no internet on the container (generally when you do on VM) , reboot the host machine
```  
apt update
```

# ADDING PROFILE GUI AND INSTALLING FIREFOX
# Installing firefox for testing gui
```
apt-get install nano firefox
```
```
nano .gui.txt
```
Copy this config of.gui.txt
```
config:
  environment.DISPLAY: :0
  raw.idmap: both 1000 1000
description: GUI LXD profile
devices:
  X0:
    path: /tmp/.X11-unix/X0
    source: /tmp/.X11-unix/X0
    type: disk
  my_gpu:
    type: gpu
name: gui
```
SAVE THE FILE as .gui.txt </br>
Create the profile
```
lxc profile create gui
```
```
lxc profile edit gui < .gui.txt
```
```
rm .gui.txt
```
```
lxc profile add HackrfJAM gui
```
```
lxc config set HackrfJAM security.privileged=true
```
```
lxc start HackrfJAM
```
```
lxc exec HackrfJAM -- bash
```
Testing GUI Firefox
```
firefox
```
## Problem of display for Quick install
Problem display at [display](https://bbs.archlinux.org/viewtopic.php?id=221449) or [pdf_display](https://github.com/SitrakaResearchAndPOC/HackrfJAM_LXD/blob/main/How%20to%20resolve%20%E2%80%9CNo%20protocol%20specified%20Unable%20to%20init%20server__%20%5BSolved%5D%20_%20Newbie%20Corner%20_%20Arch%20Linux%20Forums.pdf) </br>

* reboot the real machine :
```
rm -rf /tmp/.X11-unix/X*
```
```
reboot
```
* please reboot the container images : 
```
lxc stop  HackrfJAM
```
```
lxc start HackrfJAM
```
* listing the profile
```
lxc profile list
```
* adding the profile
```
lxc profile add HackrfJAM gui
```
* Please verify if there are two x0 and choose following ; 
```
chmod +x /tmp/.X11-unix/X0
```
```
xhost +local:
```
```
pgrep -a X
```
```
echo $DISPLAY
```
```
echo $TERM
```
* IF PROBLEM PERSIST
```
lxc profile edit gui
```
Change the number of dispaly as on the command echo $DISPLAY
```
config:
  environment.DISPLAY: :1
  raw.idmap: both 1000 1000
description: GUI LXD profile
devices:
  X1:
    path: /tmp/.X11-unix/X1
    source: /tmp/.X11-unix/X1
    type: disk
  my_gpu:
    type: gpu
name: gui
```
* remak all step on the PROBLEM OF DISPLAY
* if problem still persists ; change by other number and look at [link1]((https://bbs.archlinux.org/viewtopic.php?id=221449) [link2](https://bbs.archlinux.org/viewtopic.php?id=272491)  [link3](https://bbs.archlinux.org/viewtopic.php?id=270585)  [link4](https://bbs.archlinux.org/viewtopic.php?id=281572) [link5](https://bbs.archlinux.org/viewtopic.php?id=288581)


lxc profile create gui
   68  lxc profile edit gui < .gui.txt
   69  rm -rf gui.txt 
   70  lxc profile add BionicModulation gui
lxc config set  BionicModulation security.privileged=true

lxc stop BionicModulation

lxc start BionicModulation

lxc exec BionicModulation -- bash



RQ : xhost +x local:
ON LOCAL : 
rm -rf /tmp/.X11-unix/X0

reboot LOCAL MACHINE
chmod 777 /tmp/.X11-unix/X0

lxc stop BionicModulation

lxc start BionicModulation
 
xhost +local:
non-network local connections being added to access control list


pgrep -a X

echo $DISPLAY

export DISPLAY=$DISPLAY

lxc exec BionicModulation -- firefox



# Installing modulation dependancies : 
apt-get install hackrf gnuradio rtl-sdr ffmpeg vlc gr-osmosdr


# INSTALLING MODULATION FM



# INSTALLING OTHER MODULATION



# INSTALLING CIPHERING AES AND QUANTUM SAFE AES
