# Compiling packages for Debian and Ubuntu

As Peercoin is made to run on range of platforms, from Amazon's server to low powered Raspberry Pi Debian is perfect OS platform for deploying Peercoin nodes as it is renowned for multitude of supported hardware architectures as well as security and stability.

For compilation of Debian packages we will be using `pbuilder` which is a automatic Debian Package Building system for personal development workstation environments. pbuilder aims to be an easy-to-setup system for auto-building Debian packages inside a clean-room environment, so that it is possible to verify that a package can be built on most Debian installations. The clean-room environment is achieved through the use of a base chroot image, so that only minimal packages will be installed inside the chroot.

The following tutorial is written for the Ubuntu or Debian host, precisely Ubuntu 17.10 which is last stable version of Ubuntu at the time of writing.

## Prepare the tooling

`sudo apt install pbuilder qemu-user-static ubuntu-keyring debian-archive-keyring`

We'll also need keyring for the Raspbian, which a Debian fork made for the Raspberry Pi platform, so we can compile packages for this ARM based mini-pc platform.

> wget http://archive.raspbian.org/raspbian/pool/main/r/raspbian-archive-keyring/raspbian-archive-keyring_20120528.2_all.deb

> sudo dpkg -i raspbian-archive-keyring_20120528.2_all.deb

Now, set up the conf file for the pbuilder.

`touch .pbuilderrc`

> gedit .pbuilderrc

Paste the following:

```
#!/bin/sh

set -e

PBUILDERSATISFYDEPENDSCMD="/usr/lib/pbuilder/pbuilder-satisfydepends-apt"

if [ "$OS" == "debian" ]; then
    MIRRORSITE="http://ftp.no.debian.org/debian/"
    COMPONENTS="main contrib non-free"
    DEBOOTSTRAPOPTS=("${DEBOOTSTRAPOPTS[@]}"
        "--keyring=/usr/share/keyrings/debian-archive-keyring.gpg")
    : ${DIST:="wheezy"}
    : ${ARCH:="amd64"}
    if [ "$DIST" == "wheezy" ]; then
        #EXTRAPACKAGES="$EXTRAPACKAGES debian-backports-keyring"
        OTHERMIRROR="$OTHERMIRROR | deb $MIRRORSITE wheezy-backports $COMPONENTS"
    fi
elif [ "$OS" == "raspbian" ]; then
    MIRRORSITE="http://ftp.acc.umu.se/mirror/raspbian/raspbian/"
    COMPONENTS="main contrib non-free"
    DEBOOTSTRAPOPTS=("${DEBOOTSTRAPOPTS[@]}"
        "--keyring=/usr/share/keyrings/raspbian-archive-keyring.gpg")
    : ${DIST:="wheezy"}
    : ${ARCH:="armhf"}
elif [ "$OS" == "ubuntu" ]; then
    MIRRORSITE="http://no.archive.ubuntu.com/ubuntu/"
    COMPONENTS="main restricted universe multiverse"
    DEBOOTSTRAPOPTS=("${DEBOOTSTRAPOPTS[@]}"
        "--keyring=/usr/share/keyrings/ubuntu-archive-keyring.gpg")
else
    echo "Unknown OS: $OS"
    exit 1
fi

if [ "$DIST" == "" ]; then
    echo "DIST is not set"
    exit 1
fi

if [ "$ARCH" == "" ]; then
    echo "ARCH is not set"
    exit 1
fi

NAME="$OS-$DIST-$ARCH"

if [ "$ARCH" == "armel" ] && [ "$(dpkg --print-architecture)" != "armel" ]; then
    DEBOOTSTRAP="qemu-debootstrap"
fi
if [ "$ARCH" == "armhf" ] && [ "$(dpkg --print-architecture)" != "armhf" ]; then
    DEBOOTSTRAP="qemu-debootstrap"
fi

DEBOOTSTRAPOPTS=("${DEBOOTSTRAPOPTS[@]}" "--arch=$ARCH")
BASETGZ="/var/cache/pbuilder/$NAME-base.tgz"
DISTRIBUTION="$DIST"
BUILDRESULT="$HOME/pbuild-results/"
APTCACHE="/var/cache/pbuilder/$NAME/aptcache/"
BUILDPLACE="/var/cache/pbuilder/build"
HOOKDIR="/var/cache/pbuilder/hook.d/"
```

Make the directory where pbuilder will place the packages:

`mkdir -p $HOME/pbuild-results`

### Bootstrap the chroots

Raspbian:

> sudo OS=raspbian DIST=stretch ARCH=armhf pbuilder --create

Debian stable:

> sudo OS=debian DIST=stretch ARCH=amd64 pbuilder --create

## Preparing for build

(compiling for Raspbian stretch in this example)

Download the latest .tar.gz from github.com/peercoin.

> wget https://github.com/peercoin/peercoin/archive/v0.6.3ppc.rc1.tar.gz

Debian build system is very strict about names, so we need to rename this to:

`peercoin_0.6.3.orig.tar.gz`

Extract the contests of the file using `tar xf` and `cd` to it.

Copy the debian directory from the contrib to this directory:

`cp -r contrib/debian .`

### Some modifications

(this is just an extra step required for the Raspbian, to fix problem with autotools)

`sed '/./configure --with-gui=qt5 --with-incompatible-bdb/s/$/ --with-boost-libdir=/usr/lib/arm-linux-gnueabihf/' debian/rules`

## Building the package

`OS=raspbian DIST=stretch ARCH=armhf pdebuild`

And wait, it will take a while so go get a coffee or something. It's compiling by emulating ARM cpu in QEMU.

The concept of pbuild and cross-platform compilations is that you pass it this environment variables like "OS" and "DIST".

For example OS=debian and DIST=wheezy will use Debian Wheezy chroot, you can also pick architecture by using ARCH= environment variable.

__________________________________________________

source: https://jodal.no/2015/03/08/building-arm-debs-with-pbuilder/