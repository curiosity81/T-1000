# Project T-1000

## Aim
Build a message signing device so that:

0. The device fits into a pocket.
1. The total cost is around 1000 cent.
2. The hard- and software is open source.
3. The device is as secure as possible.

## WARNING
THIS DOCUMENT DOES NOT CLAIM TO BE COMPLETE!!! THIS IS ONLY A PROOF OF CONCEPT. ONLY STORE IMPORTANT DATA ON THE DEVICE IF YOU KNOW WHAT YOU ARE DOING.

## Introduction
If a person wants to proof its (online) identity without revealing its true identity, modern asymmetric cryptography is essential.
Messages can simply be signed with the private key whose public key is publicly associated to the person's (online) identity.
For instance, the person could publish a bitcoin address on the internet, for which it owns the private key.
Messages signed with the private key can then be verified by others on the internet.
To create such a signed message via bitcoin core is simple and can be done quickly using bitcoin-qt.
In this case, the private key is stored in the wallet.dat file.
But this method can be problematic so that the following points are extremly important:

1. The wallet MUST be encrypted.
2. The home folder must be encrypted.
3. The partition should be encrypted.

However, this does not help, if the wallet was stored in the profile of a normal and the internet browsing user, whose profile or computer might be compromised in one way or another.
Solutions to this problem:

1. Usage of an hardware wallet.
2. Usage of a second computer in the private LAN (without internet connection!) only for handling the private keys.

If the first point applies to you, that is you already own an hardware wallet, then you can stop reading here.
The second point can clearly be a waste of energy, hardware and space, especially, if the second computer does not consist of specific hardware.
This is where project T-1000 comes into play:
Project T-1000 stands for "project Trezer0-1000", a simple open source and raspberry pi zero based Trezor alternative, small enough to fit into a pocket.
Why using a rasperry pi zero?

0. It is small and has roughly the size of an usb-stick.
1. It is cheap and only costs around 5$.
2. It is a stand-alone computer and thus, as flexible as possible with respect to software and additional hardware.
3. Energy for the device and control over the device are provided via the same usb-connection.

## Material
0. Ubuntu 16.04.03 LTS
1. Raspberry pi zero
2. Micro sd card
3. Usb cable
4. 3D-printer (optional)

## Methods

### Install Raspbian
Enter the Download directory:
```
cd /home/<user>/Downloads
```
Download the current version of [Raspbian](https://www.raspberrypi.org/downloads/raspbian/):
```
wget https://downloads.raspberrypi.org/raspbian_latest
```
This will save a file with the name "raspbian_latest", which represents a zip-archive.
Rename it:
```
mv raspbian_latest raspbian_latest.zip
```
Test the sha256-hash of the zip-archive:
```
sha256sum raspbian_latest.zip | grep -o 64c4103316efe2a85fd2814f2af16313abac7d4ad68e3d95ae6709e2e894cc1b
If grep returns the hash, everything is fine.
```
Unzip it:
```
unzip raspbian_latest.zip
```
The current Raspbian image will be unzipped in the Downloads-directory, e.g:
```
2017-11-29-raspbian-stretch.img
```
Now insert the micro sd card into your computer, e.g. by means of a mirco sd card adapter.
Check via gparted (sudo apt-get install gparted) which device name the sd card has:
```
sudo gparted
```

BE CAREFUL AND DO NOT MIX THE PARTITIONS, IN THE WORST CASE YOU INSTALL RASPBIAN ON YOUR MAIN PARTITION!

Close gparted.
If you have identified the correct device (something like /dev/sdb or /dev/sdc), write the Raspbian image to the sd card:
```
sudo dd if=2017-11-29-raspbian-stretch.img of=/dev/<the_identified_device>
``` 
Then remove the sd card from the computer and insert it again.
Two new file systems should automatically pop up.
```
cd /media/<user>/boot
```
Do the [following](https://www.thepolyglotdeveloper.com/2016/06/connect-raspberry-pi-zero-usb-cable-ssh/):
```
sudo touch ssh
```
And
```
sudo nano config.txt
```
Add the following line at the bottom of the file:
```
dtoverlay=dwc2
```
Exit nano via Ctrl+x and press y for accepting the changes.
```
sudo nano cmdline.txt
```
Find "rootwait" in the file and add
```
modules-load=dwc2,g_ether
```
directly behind it, delimited with exactly one space, but make sure to also keep the other stuff.
The result should look as follows:
```
... rootwait modules-load=dwc2,g_ether quiet ...
```
Exit nano via Ctrl+x and press y for accepting the changes.
Leave the current directory:
```
cd /home/<user>/Downloads
```
Unmount the two file systems on the sd card by right clicking on the corresponding symbols on the unity bar on the left by selecting "Unmount".
Insert the sd card into the raspberry pi zero.
Insert the usb-cable into the micro usb port of the pi, which is closest to the middle.
The device is now ready for its first boot up.

### Connect to raspberry pi zero
Plug the device into an usb-port of your computer and wait around two minutes.
Do a right click on the network manager (right top, close to, where the unity windows manager shows the time: the icon with one arrow up and one arrow down if you are connected to the internet).
Some of the shown information will double there, but not in a reasoned way (a kind of ms-windows behavior ...).
Since there is no configured connection to the raspberry pi zero yet, let's create one:
Click on "Edit Connections..." -> "Add" -> "Ethernet" -> "Create" -> "IPv4 Settings" (you can also give the new connection a meaningful name).
Now, there are two possible configurations under "Method" we will use:

1. "Link-Local Only"
2. "Shared to other computers"

If the device is not allowed to have an internet connection, then select the first possibility (you will be still able to access the device via ssh).
This configuration is used later on, when the device is readily installed and configured.
However, since Raspbian should be updated and additional software needs to be downloaded, we select the second possibility.
Click "Save" and "Close" and Ubuntu will do the rest.
In a terminal check:
```
ifconfig
```
This command should show a new ethernet device with an ip assigned.
Now connect to the device via ssh:
```
ssh pi@raspberrypi.local
```
Password is "raspberry" by default.
Note, that Ubuntu seems to have problems to select the correct ethernet connection after its reboot.
That is, Ubuntu mixes up the internet connection with the newly created raspberry pi zero connection.  
Therefore, delete an old raspberry pi zero connection before you insert the device into the usb-port of your computer and then follow the steps of this paragraph from the beginning.

### Configure raspberry pi zero
After logging into the device, do:
```
sudo raspi-config
```
You can browse the [raspi-confi](https://www.raspberrypi.org/documentation/configuration/raspi-config.md) menu via arrow, tab and return key.
Choose "Expand file system" so that the device will use all of the sd card's memory.
This change will apply after reboot.
Also set the "Localisation options":

1. Set "Change local" to, e.g., "en_GB.UTF-8 UTF-8".
2. Set the "Time zone" to the time zone where you are living in.
3. If you use a specific keyboard, also adapt "Change keyboard layout" correspondingly.

Finish the tool.
Then reboot:
```
sudo shutdown -r now
```
After reboot update Raspbian (if there are problems with logging into the device again, see the end of paragraph "Connect to raspberry pi zero"):
```
sudo apt-get update
```
Followed by
```
sudo apt-get dist-upgrade
```
The upgrade procedure will now take some time, grab a coffee, a beer or a glass of wine and do something else in the meantime.

### Compile bitcoin core
http://raspnode.com/diyBitcoin.html

### Change default user
Bla fasel.

### Install firewall
Bla fasel.

### Configure wallet
Bla fasel.

### Case

Download the 3D-model for the case [here](https://www.thingiverse.com/thing:1436545).
You can use the original model, but then the sd card can be removed from the device easily.
An improved version can be derived using the 3D-modeling software [OpenScad](http://www.openscad.org/) (sudo apt-get install openscad) as follows.
Firstly, change the PiCase-Cover model and save the result in a new file:
```
import("/<path_to_model>/Raspberry_Pi_Zero_Keychain_Case/files/PiCase-Cover.stl", convexity=3);

translate([-36.5,-16.5,-4.75]){
    cube([2.5,33,1.5]);
}
```
Secondly, change the PiCase model and save the result in a new file:
```
import("/<path_to_model>/Raspberry_Pi_Zero_Keychain_Case/files/PiCase.stl", convexity=3);

translate([-36.5,-16.5,-3.25]){
    difference(){
        cube([2.5,33,6.5]);
        translate([1.25,11.9,3]){
            cube([2,13,10]);
        }
    }
}
```
The code above will work if the downloaded 3D-model is still available and was not changed in the meantime.
Print the case.

### Misc
(https://www.raspberrypi.org/documentation/configuration/security.md)
https://www.raspberrypi.org/forums/viewtopic.php?t=37324
https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server

## Conclusion
Bla fasel.
