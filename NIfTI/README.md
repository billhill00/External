To build the NIfTI c library.

Prerequisites: To build nifticlib-2.0.0 requires cmake

1. Unpack the sources:
     tar -zxf nifticlib-2.0.0.tar.gz
2. Configure using either cmake or cmake-gui with the build directory the
   same as the source directory (nifticlib-2.0.0) and setting the install
   prefix (eg /opt/MouseAtlas):
     cmake-gui
   or
     cmake -i
   If building JavaWoolz "-fPIC" will need to be set for the cmake compiler
   flags.
3. Build the libs:
     cd nifticlib-2.0.0
     make
4. Install the software
     make install
