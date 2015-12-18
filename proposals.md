On Thu, Dec 17, 2015 at 11:47 AM, Jos Poortvliet <jospoortvliet@gmail.com> wrote:
>  Love the energy! There are many proposals. Of course, many conflicting, going in different directions - building on resin.io, with Arch, building on Debian and the Freedombox, building on Ubuntu.
>
> I don't want you to think of this as a contest! *It is not*. We should try to find *common ground*.

Absolutely! I'll try to flesh out the current options on various parts of the stack as proposed by various people in this email so that we can have a central place to discuss them and hopefully reach some consensus.

The rest of the email is structured around the main components of the stack for which different options have been proposed. I tried to include everything proposed so far but if I left something out please reply to this email and add it :) Also, different options aren't necessarily mutually exclusive, we might end up having more than one from each section.

The main components are:

- Root filesystem
- Operating system
- Packaging
- Initial config
- HTTP Server
- Database engine
- Database storage
- Caching
- Backups
- External projects

At the end, there is a Miscelaneous category where I put various smaller ideas that were proposed.

Ok, here we go...

Root filesystem
---------------

### squashfs+overlayfs
Proposed by:
	* Michal Hrusecky

### ext4

### btrfs

Operating system
----------------

### Debian/Raspbian

Proposed by:
	* Boris Rybalkin

### Freedom-box

Supports Beaglebone, Cubiebox/Cubietruck, various Raspberry Pi models (including the RPi2) and others

The freedom-box project is an effort to move social networking and other centralised services to a more P2P model that respects user freedom and gives the user control over where their data goes and, particularly, doesn't.

Proposed by:
    * Johan Ouwerkerk

### ArchLinux ARM

Supports BeagleBoard, Beaglebone Black, Cubie{board, board 2, truck} RPi{1,2}, ODROID-{U2,U3,X,X2,XU,XU3,XU4} and more

Proposed by:
    * Petros Angelatos

### TinyCore Linux

Runs from RAM, 15 seconds boot time, 100MB usage with Apache + PHP
http://ska.ee/posts/2015/2015-12/2015-12-07_philecms_picore_eng

Proposed by:
   * Artjom Tsarajev

### openSUSE
Proposed by:
   * Michal Hrušecký

Packaging
---------

### Packages

#### Raspbian
* Old version of owncloud (7.0)
* Old version of PHP (5.6)

#### ArchLinux ARM
* Latest version of ownCloud (8.2)
* Old version of PHP (5.6)

Proposed by:
	* Petros Angelatos

#### openSUSE

#### TinyCore Linux

### Containers

#### Docker

#### systemd-nspawn

Initial config
--------------

### mDNS (avahi)

Use mDNS/DNS-SD (Avahi/Bonjour) to auto-publish the box to the local network. This would permit 'apps' to auto-discover the box. It will also allow a browser running on another computer on the local network to access the initial setup interface at a well-known address (for example owncloud.local).

Proposed by:
    * Alex-P. Natsios
    * Johan Ouwerkerk
    * Petros Angelatos
    * Salih Emin
    * Stathis Iosifidis
    * Thanos Tryfonidis
	* Michal Hrušecký

### IPv6 link-local addresses

Note: Relies on client and local network support for IPv6.

Note: Raspberry Pis don't have printed MAC information, someone will have to boot them up, get it, print it on the box, and ship it.

This also uses a web interface to do the initial config but instead of using a mDNS domain it uses the MAC address of the device to generate a link-local IPv6 address and then connects to it. The user will initially visit a well known URL (for example pidrive.owncloud.org) which will host a simple HTML page where you enter the MAC address and then redirects you to the link-local IPv6 address.

Proposed by:
    * Johan Ouwerkerk

### WiFi Access point

Note: This is implemented in the Prota OS project

Puts RPi with WiFi dongle into the AP mode, so users can find Pi in their WiFi SSID list and connect to it. Then, they open up a web browser to configure Pi's WiFi using aweb-based interface.

Proposed by:
    * Terence Park

### Mobile application

Note: This is implemented in the Syncloud project

Note: This can be combined nicely with the Avahi option

The user downloads a app on his android or iOS device to set up my ownCloud server. The app discovers the servers on the local network and presents setup and information interfaces. It shouldn't require prior technical knowledge to complete the setup.

Proposed by:
	* Mickaël Fourgeaud

HTTP server
----------

### apache2

Proposed by:
    * Jos Poortvliet
	* Christian Rost

### nginx

Proposed by:
	* Daniel Ripoll 

Database engine
---------------

### MySQL

Proposed by:
	* Jos Poortvliet

### SQLite

Proposed by:
	* Michal Hrusecky

Database storage
----------------

### SD card

Proposed by:
	* Michal Hrusecky

### Hard Disk

Proposed by:
	* Jos Poortvliet

Caching
-------

### Redis

### Plain PHP caching

External projects
-----------------

### Syncloud

* Support for several major ARM SBCs (Raspberry Pi 2, Beagle Bone Black, Cubieboard 2, Cubietruck and ODROID XU3/XU4)
* Debian based root partition
* Runs avahi on the device and there are apps for Android and iOS that use it to discover ownCloud devices in the local network
* Automatic dynamic DNS using Amazon Route53
* UPnP and NAT-PMP protocols are used to map ports on the home router

Proposed by:
	* Boris Rybalkin

### onmydisk.org

### Buildroot
### FUSE over SSL

Proposed by:
    * Alexey Volkov

### resin.io

#### Yocto
### Prota OS
 Prota provides a service called App Library, from which users can download and install pre-packaged applications to their Protas. There will be a OwnCloud application there.

 Prota has its own automation engine, sort of similar to IFTTT, but a lot more powerful as it runs on your own hardware (this means you can utilize Pi's GPIO and plug in any sensors of your choice).
 
 Work needed
 1. Port the latest version of ownCloud to the latest version of Prota OS.
 2. Integrate ownCloud to Prota's automation engine.

Proposed by:
	* Terence Park

Miscelaneous
------------

### The general idea is to modify the current "Owncloud Sync" app to be the Control center of the WDSata+Raspberry PI+owncloud Hub.

1. We will be adding a button to the syncing software. When the user
installs and lauches the software, he will be presented with a welcome
screen plus the network discovery button that will scan the network
and find the IP and important details of the WD-oC box. Primary goal
would be  to build a feature that will be linking the user's computer
with the box (and adding it as a cloud drive option).

Proposed by:
    * Alex-P. Natsios
    * Salih Emin
    * Stathis Iosifidis
    * Thanos Tryfonidis

### Samba server
	* Michal Hrušecký
    * Alex-P. Natsios
    * Salih Emin
    * Stathis Iosifidis
    * Thanos Tryfonidis

###  ftp server sharing users database and allowing direct access to the files. Or maybe localhost mounted wdfs exported via ftp/ssh so rsync would be possible.
	* Michal Hrušecký

###  hot things like multiple boards support, host OS updates, data backup are not implemented yet. In collaboration with redis.io we could make it really good.
    * Alexey Volkov

### dynDNS
### Antivirus (clamav) (mod_sec)
### UPnP
### Let's Encrypt SSL certs
### ownBackup / backup solution
### Automated Updates (Host OS) (ownCloud via updater)
	* Christian Rost

### include IPv6 (either tunnel or maybe 6to4)
	* Michal Hrušecký
