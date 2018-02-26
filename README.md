# Project T-1000

## Aim
Build a message signing device so that:

0. The device fits into a pocket.
1. The total cost is around 1000 cent.
2. The hard- and software is open source.
3. The device is as secure as possible.

WARNING: THIS DOCUMENT DOES NOT CLAIM TO BE COMPLETE!!! ONLY STORE IMPORTANT DATA ON THE DEVICE IF YOU KNOW WHAT YOU ARE DOING.

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

### Install raspian
Bla fasel.

### Connect to raspberry pi zero
Bla fasel.

### Configure raspberry pi zero
Bla fasel.

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
