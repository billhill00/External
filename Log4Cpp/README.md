#!/bin/sh
# \file         README-Log4cpp
# \author       Bill Hill
# \date         January 2012
# \version      $Id$
#
# To build the Log4cpp libraries for the Woolz applications follow the
# steps below or copy edit and run this script.

set -x

# setenv MA ~/MouseAtlas/Build/
#export MA=~/MouseAtlas/Build/
export MA=/opt/MouseAtlas/
# set path = ("$MA"/bin $path)
export PATH="$MA"/bin:$PATH
# setenv LD_LIBRARY_PATH "$MA"/lib:$LD_LIBRARY_PATH
export LD_LIBRARY_PATH="$MA"/lib:$LD_LIBRARY_PATH

# Cleanup
rm -rf log4cpp-1.0

# Unpack archive and patch
tar -zxf log4cpp-1.0.tar.gz
patch -p0 < log4cpp-1.0.patch

# Configure for use with Woolz
cd log4cpp-1.0
./configure --prefix $MA \
            --disable-shared \
	    --enable-static \
	    --with-pic

make
make install
cd ..

# Cleanup
# rm -rf log4cpp-1.0

