# Project T-1000

## Aim
Build a message signing device so that:
0. The device fits into a pocket.
1. The total cost is around 1000 cent.
2. The hard- and software is open source.
3. The device is as secure as possible.

WARNING: THIS TUTORIAL DOES NOT CLAIM TO BE COMPLETE!!! ONLY STORE IMPORTANT DATA ON THE DEVICE IF YOU KNOW WHAT YOU ARE DOING.

## Introduction
If a person wants to proof its (online) identity without revealing its true identity, modern asymmetric cryptography is essential.
Messages can simply be signed with the private key derived from a public key associated to the person's (online) identity.
For instance, the person could publish a bitcoin address on the internet, for which it owns the private key.
Messages signed with the private key can then be verified by others on the internet.
To create a message via bitcoin core is simple and can be done quickly using bitcoin-qt.
In this case, the private key is stored in the wallet.dat file.
But this method can be problematic so that the following points are extremly important:
1. The wallet MUST be encrypted.
2. The home folder must be encrypted.
3. The partition should be encrypted.
However, this does not help, if the wallet was stored on the normal browsing computer, which might be compromised in one way or another.
Solutions to this problem:
1. Usage of an hardware wallet.
2. Usage of a second computer in the private LAN only for handling the private keys.
If the first point applies to you, that is you already own an hardware wallet, then you can stop reading here.
The second point can clearly be a waste of energy, hardware and space, especially, if the second computer does not consist of specific hardware.
This is where project T-1000 comes into play:
Project T-1000 stands for "project Trezer0-1000", a simple open source and raspberry pi zero based Trezor alternative, small enough to fit into a pocket.
Why using a rasperry pi zero?
0. It is small and has roughly the size of an usb-stick.
1. It is cheap and only costs around 5$.
2. It is a real computer and thus, as flexible as possible with respect to software and additional hardware.
3. Energy for the device and control over the device are provided via the same usb-connection.

## Material
1. raspberry pi zero
2. micro ssd card
3. usb cable
4. 3D-printer (optional)

## Methods

### Install raspian

### Connecting to raspberry pi zero

### Install bitcoin core
http://raspnode.com/diyBitcoin.html

### Misc
(https://www.raspberrypi.org/documentation/configuration/security.md)
https://www.raspberrypi.org/forums/viewtopic.php?t=37324
https://www.digitalocean.com/community/tutorials/how-to-setup-a-firewall-with-ufw-on-an-ubuntu-and-debian-cloud-server

## Conclusion
Bla fasel
