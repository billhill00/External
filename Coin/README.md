#!/bin/sh
# \file         README-Coin
# \author       Bill Hill
# \date         January 2013
# \version      $Id$
#
# The Coin and SIMVoleon were both derived from the bitbucket
# repository (https://bitbucket.org/Coin3D/) but with both
# local and bitbucket/github contributions for bug fixes.
# Where bug fixes have been made the original file is
# preserved with the .orig extension added.
# SoQt was also originaly downloaded from bitbucket.
# To build Coin, SIMVoleon and SoQt for the Woolz applications
# follow the steps below or copy edit and run this script.

set -x

#setenv MA ~/MouseAtlas/Build/
#export MA=~/MouseAtlas/Build/
#export MA=~/MouseAtlas/Build/debug
export MA=/opt/MouseAtlas/
# set path = ("$MA"/bin $path)
export PATH="$MA"/bin:$PATH
# setenv LD_LIBRARY_PATH "$MA"/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$MA"/lib:$LD_LIBRARY_PATH

# Cleanup
rm -rf *-build Coin3D-20111204 SIMVoleon-20111204 SoQt-1.5.0

# Unpack archives
tar -zxf Coin3D-20111204.tar.gz
tar -zxf SIMVoleon-20111204.tar.gz
tar -zxf SoQt-1.5.0.tar.gz

# Build Coin
rm -rf Coin3D-20111204-build
mkdir Coin3D-20111204-build
cd Coin3D-20111204-build
# for OSX add --with-framework-prefix=$MA/frameworks
../Coin3D-20111204/configure --prefix=$MA \
			--disable-dl-openal \
			--disable-dl-freetype \
			--disable-dl-fontconfig \
			--enable-optimization \
			--enable-threadsafe \
			--enable-static \
			--disable-shared \
	    		--with-pic \
			--disable-debug
make
make install
cd ..

# Build SIMVoleon
rm -rf SIMVoleon-20111204-build
mkdir SIMVoleon-20111204-build
cd SIMVoleon-20111204-build
../SIMVoleon-20111204/configure --prefix=$MA \
                             --enable-optimization \
			     --enable-threadsafe \
			     --enable-static \
			     --disable-shared \
	    		     --with-pic \
			     --disable-debug

# Note: If linking error is generated (on Linux 64) related to crti.o then
# edit build/libtool and comment out the predep_objects and postdep_objects
# lines containing crti.o, eg
# vi +/crt'[in]'.o libtool
# or
# sed -i orig -e 's/^\(p...*dep_objects *= *"...*"\)/# \1/' libtool

make
make install
cd ..

# Build SoQt
rm -rf SoQt-1.5.0-build
mkdir SoQt-1.5.0-build
cd SoQt-1.5.0-build
# for OSX add --with-framework-prefix=$MA/frameworks
../SoQt-1.5.0/configure --prefix=$MA \
			--enable-optimise \
			--enable-static \
			--disable-shared \
			--with-pic \
			--disable-debug
make
make install
cd ..

# Cleanup
# rm -rf *-build Coin3D-20111204 SIMVoleon-20111204 SoQt-1.5.0
