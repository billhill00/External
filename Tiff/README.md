#!/bin/sh
# \file         README.Tiff
# \author       Bill Hill
# \date         January 2012
# \version      $Id$
#
# To build the Tiff libraries for the Woolz applications follow the
# steps below or copy edit and run this script.

# setenv MA ~/MouseAtlas/Build/
#export MA=~/MouseAtlas/Build/
export MA=/opt/MouseAtlas/
# set path = ("$MA"/bin $path)
export PATH="$MA"/bin:$PATH
# setenv LD_LIBRARY_PATH "$MA"/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$MA"/lib:$LD_LIBRARY_PATH

# Cleanup
#rm -rf tiff-4.0.8

# Unpack archive
#tar -zxf tiff-4.0.8.tar.gz

# Configure for use with Woolz
cd tiff-4.0.8
./configure --prefix=$MA \
            --disable-shared \
	    --enable-static \
	    --with-pic \
	    --with-jpeg-include-dir=$MA/include \
	    --with-jpeg-lib-dir==$MA/lib

make
#make install
cd ..

# Cleanup
# rm -rf tiff-4.0.8
