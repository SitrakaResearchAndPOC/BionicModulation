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
lxc profile add  BionicModulation gui
```
```
lxc config set  BionicModulation security.privileged=true
```
```
lxc start  BionicModulation
```
Testing GUI Firefox
```
lxc exec  BionicModulation -- firefox
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
lxc stop  BionicModulation
```
```
lxc start  BionicModulation
```
* listing the profile
```
lxc profile list
```
* adding the profile
```
lxc profile add  BionicModulation gui
```
* Please verify if there are two x0 and choose following ;
You could verify using
```
lsof -U | grep X1
```

```
chmod +x /tmp/.X11-unix/X0
```
```
xhost +local:
```
non-network local connections being added to access control list
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
* if problem still persists ; change by other number and look at : </br> [link1](https://bbs.archlinux.org/viewtopic.php?id=221449) </br>[link2](https://bbs.archlinux.org/viewtopic.php?id=272491)  </br> [link3](https://bbs.archlinux.org/viewtopic.php?id=270585) </br> [link4](https://bbs.archlinux.org/viewtopic.php?id=281572) </br> [link5](https://bbs.archlinux.org/viewtopic.php?id=288581) </br>
```
lxc exec BionicModulation -- firefox
```

# INSTALLING DEPENDANCIES MODULATIONS
```
lxc exec BionicModulation -- bash
```
```
apt-get install hackrf gnuradio rtl-sdr ffmpeg vlc gr-osmosdr
```
```
apt-get install git unzip
```

# INSTALLING MODULATION FM
(sing : vazo sihanaka sambiavy an'i zoky be leon paul)
```
mkdir FM-Modulation
```
```
cd FM-Modulation
```
Downloads as on the [link](https://github.com/SitrakaResearchAndPOC/FM_Transmitter/tree/main) </br>
```
wget https://media.githubusercontent.com/media/SitrakaResearchAndPOC/fork_fm_transmitter/main/FM_Transmitter.zip
```
```
unzip FM_Transmitter.zip
```

# PLUG HACKRF AND ADD IT ON THE CONTAINER
```
git clone --depth 1 https://github.com/henintsoa98/QCSuperLXD  
```
```
cd QCSuperLXD
```
If it's not run, the fork project is at [fork](https://github.com/SitrakaResearchAndPOC/fork_QCSuperLXD)
```
chmod +x lxd-device lxd-image  
```
```
sudo cp lxd-device lxd-image /usr/local/bin
```
```
cd ..
```
```
rm -rf QCSuperLXD  
```
```
exit
```
## plug your rooted device and enable adb debugging
```
lxd-device add BionicModulation hackrftransmit
```
## select an number that is your device in the list
Have a look on this [image](https://github.com/SitrakaResearchAndPOC/QCSuper/blob/main/screen2.jpg)

## run gnuradio 
```  
lxc exec BionicModulation -- gnuradio-companion
```

## configure file source and osmosdr and hackrf on osmosdr: 
Tape CTRL+SHIFT + T for new terminal
```  
lxc exec BionicModulation -- hackrf_info
```
Just memorize the number serial of hackrf

Change the file source and the osmosdr block


# INSTALLING OTHER MODULATION
```
git clone https://github.com/SitrakaResearchAndPOC/BionicModulation
```

# INSTALLING CIPHERING AES AND QUANTUM SAFE AES
```
lxc exec BionicModulation -- bash
```
```
apt update
```
```
apt-get install python3-pip wget
```
```
apt-get install python3-pip
```
```
pip3 install progressbar
```
```
pip3 uninstall numpy
```
```
pip3 install "numpy<1.20.0"
```
```
apt install python3-distutils
```
#pip3 install click </br>
#https://segmentfault.com/a/1190000040609361 </br>
```
pip3 install "click>7.1.0"
```
```
pip3 show click
```
```
pip3 install progress
```
```
pip3 install sympy
```
```
pip3 install Exit
```
```
sudo apt install -y dh-python python3-click python3-progress  python3-numpy python3-matplotlib python3-networkx   python3-stdeb python3-setuptools-scm python3-setuptools python3-cpuinfo
pip3 install dh click numpy progress matplotlib networkx stdeb setuptools-scm setuptools
```
```
sudo apt-get install python-all
```
## constant time csurf and crads
```
git clone https://github.com/Krijn-math/Constant-time-CSURF-CRADS
```
```
cd Constant-time-CSURF-CRADS/
```
```
python3 main.py --help
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd1 -v -a csidh -e 10
```
```
python3 main.py -p p512  -m scaled -s wd2 -v -a csidh -e 5
```
```
python3 main.py -p p512  -m unscaled -s wd2 -v -a csurf -e 5
```
FOR MORE EXAMPLE PLEASE SEE [fork Constant-time-CSURF-CRADS](https://github.com/SitrakaResearchAndPOC/fork_Constant-time-CSURF-CRADS) or[original Constant-time-CSURF-CRADS](https://github.com/Krijn-math/Constant-time-CSURF-CRADS)
```
cd ..
```


## installing sibc
```
git clone https://github.com/JJChiDguez/sibc
```
```
cd sibc
```
```
python3 setup.py bdist_deb
```
```
sudo python3 setup.py install
```
```
python3 sibc csidh-bench
```
```
python3 sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
```
sibc -p p512 -f hvelu -a csidh -s df -e 10 csidh-main
```
## Testing : 
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/real_csidh.py
```
```
python3 real_csidh.py 
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/real_csidh.py
```
```
python3 real_csidh.py 
```

Launching separate mode for csidh sibc
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/keygen_csidh_sibc.py
```
```
wget https://raw.githubusercontent.com/SitrakaResearchAndPOC/Cryptodome/main/shared_csidh_sibc.py
```
```
rm -rf *.pub *.priv *.key
```
```
python3 keygen_csidh_sibc.py -n alice
```
```
ls
```
```
python3 keygen_csidh_sibc.py -n bob
```
```
ls
```
```
python3 shared_csidh_sibc.py -p alice.pub -s bob.priv -k key1.key
```
```
python3 shared_csidh_sibc.py -p bob.pub -s alice.priv -k key2.key
```
# TESTING AES AND QUANTUM SAFE AES
```
git clone https://github.com/SitrakaResearchAndPOC/Python_PQAES_FO.git
```
```
cd Python_PQAES_FO/
```
```
unzip Python-PQAES.zip 
```
```
cd Python-PQAES-CSIDH/
```
```
python3 AES.py -e test.txt -c 128
```
```
python3 AES.py -d test.txt.aes -c 128
```
```
Name the decrypted file as test_dec.txt
```
```
tail -f test_dec.txt
```
```
python3 FO.py 
```
```
python3 FO.py -e test.txt -a sha256 -k bob.priv 
```
```
python3 FO.py -d test.txt.fo -a sha256 -k bob.priv 
```
```
tail f test_fo.txt 
```
```
python3 PQAES.py
```
# For publishing image
```
lxc publish BionicModulation --alias BionicModulation -f
```
Instance published with fingerprint: 3b1b00e67439adbe6d6228dc9fd9e05c1463bbafd64b2e0438bcb499e8274211
```
lxc image export BionicModulation .
```
```
md5sum 3b1b00e67439adbe6d6228dc9fd9e05c1463bbafd64b2e0438bcb499e8274211.tar.gz
```

