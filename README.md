# Student Edition ModelSim on Debian, maybe Ubuntu. (why is ModelSim 32-bit???)

Hello! This is an installation tutorial that works on Debian as of 2 October 2020, and probably other Debian-based distros like Ubuntu.

I used an online instruction set (link at the bottom), but some things didn't work so I had to slightly modify the instructions.

Please raise an issue if this does not appear to work for you.

## Install Dependencies

$ sudo dpkg --add-architecture i386

$ sudo apt-get install libxi6:i386 libncurses6

$ sudo apt-get install libc6:i386 libncurses5:i386 libstdc++6:i386 lib32z1

$ sudo apt-get install build-essential gcc-multilib g++-multilib lib32stdc++6 lib32gcc1 expat:i386 fontconfig:i386 libfreetype6:i386 libexpat1:i386 libgtk-3-0:i386 libcanberra0:i386 libpng12-0:i386 libice6:i386 libsm6:i386 zlib1g:i386 libx11-6:i386 libxau6:i386 libxdmcp6:i386 libxext6:i386 libxft2:i386 libxrender1:i386 libxt6:i386 libxtst6:i386

## Install ModelSim Files

In some directory, download ModelSimSetup-16.1.0.196.run

## Install and Build Freetype Library

cd to some other directory, install the Freetype library source code http://download.savannah.gnu.org/releases/freetype/freetype-2.4.12.tar.bz2

$ tar -xvf freefreetype-2.4.12.tar.bz2

$ sudo apt-get build-dep -a i386 libfreetype6

cd to the directory where you extracted freetype-2.4.12

$ ./configure --build=i686-pc-linux-gnu "CFLAGS=-m32" "CXXFLAGS=-m32" "LDFLAGS=-m32"

$ make -j8

## Final Setup

cd to the directory with ModelSimSetup

$ chmod +x ModelSimSetup-16.1.0.196.run

$ ./ModelSimSetup-13.1.0.162.run (instead of ./ModelSimSetup-13.1.0.162.run install Modelsim)

cd to ./modelsim_ase

$ mkdir lib32

cp with sudo or root privileges, directory/that/contains/freetype-2.4.12/objs/.libs/libfreetype.so* ./lib32

cd to ./modelsim_ase/bin and edit vsim with sudo or root privileges (because vsim is in read-only mode)

in vim, in the first non-comment line, change: **mode=${MTI_VCO_MODE:-""}** -> **mode=${MTI_VCO_MODE:-"32"}**

type /rh, (or in another text editor search the line with vco="linux_rh60") and change: **vco="linux_rh60"** -> **vco="linux"**))

right after the line with **dir=\`dirname $arg0\`**, add **export LD_LIBRARY_PATH=${dir}/lib32**

Finally, running ./vsim should open ModelSim.



original instructions: https://profile.iiita.ac.in/bibhas.ghoshal/COA_2020/Lab/ModelSim%20Linux%20installation.html

installer location: https://drive.google.com/file/d/0BxghKvvmdklCSm0yTFJJYjNYQXM/view

Last Updated: 2 October 2020 16:00 UTC−07:00
