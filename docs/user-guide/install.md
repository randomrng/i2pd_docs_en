Installing
==========

Building from source
--------------------

See [developer section documentation](../devs/building/requirements.md) for how to build i2pd from source on your OS.


Windows, Android, Mac OS X  
--------------------------

The easiest way to install i2pd is by using precompiled binaries. 
Go to the [latest release page](https://github.com/PurpleI2P/i2pd/releases/latest) and choose a file for your operating system.


## Docker images

You can use our [prebuilt docker images](https://hub.docker.com/r/purplei2p/i2pd/).

    docker pull purplei2p/i2pd


## Ubuntu

You can install binary packages from the [latest release page](https://github.com/PurpleI2P/i2pd/releases/latest). 

Alternatively, you can use [PPA repository](https://launchpad.net/~purplei2p/+archive/ubuntu/i2pd) run by PurpleI2P community member [R4SAS](https://twitter.com/i2pr4sas).

    sudo add-apt-repository ppa:purplei2p/i2pd
    sudo apt-get update
    sudo apt-get install i2pd


## Debian

Look for Debian packages at the [latest release page](https://github.com/PurpleI2P/i2pd/releases/latest).

Alternatively, you can install i2pd by using repository run by PurpleI2P community member [R4SAS](https://twitter.com/i2pr4sas).

Add repository to /etc/apt/sources.list:

    # Debian 7
    deb http://repo.lngserv.ru/debian wheezy main
    deb-src http://repo.lngserv.ru/debian wheezy main
    # Debain 8
    deb http://repo.lngserv.ru/debian jessie main
    deb-src http://repo.lngserv.ru/debian jessie main

Import key that is used to sign the release:

    gpg --keyserver keys.gnupg.net --recv-keys 98EBCFE2
    gpg -a --export 98EBCFE2 | sudo apt-key add -

After that you can install i2pd as any other software package:

    apt-get update
    apt-get install i2pd

Look for more information about Debian repository [here](https://repo.lngserv.ru/.help/readme.txt).


## ArchLinux

i2pd packages are available at AUR: [release version](https://aur.archlinux.org/packages/i2pd/),
[nightly builds](https://aur.archlinux.org/packages/i2pd-git/)

## Gentoo Linux

Install from Gentoo repository: [i2pd package](https://packages.gentoo.org/packages/net-vpn/i2pd).


FreeBSD
-------

You can install i2pd from [ports](https://www.freshports.org/security/i2pd/).

