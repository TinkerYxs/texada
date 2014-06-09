# Texada Readme

### Directory Structure

      Texada
         /bin  -- created by makefile
            /src -- contains src objects
            /tests -- contains test objects
         /src -- source code for main project
         /tests -- main project tests

### Required Libraries

Texada relies on two non-standard libraries, [SPOT](http://spot.lip6.fr/wiki/GetSpot) and [Google Test](https://code.google.com/p/googletest/). 

Google Test can be used in Eclipse if the C/C++ Unit Testing Support item, which can be installed along with the CDT. To install the CDT and Unit Testing Support, add the website http://download.eclipse.org/tools/cdt/releases/youreclipseversion to the Help->Install New Software... dialogue, with youreclipseversion replaced by your eclipse version (e.g. Kepler). The C/C++ Unit Testing Support can then be installed under CDT Optional Features.

To install SPOT, navigate to the link above and download the tar.gz file. Extract the spot-version.tar.gz file where you'd like it to be. This can be done via the tar command:

tar -zxvf spot-version.tar.gz

Note that SPOT requires the instllation of the [Boost](http://www.boost.org/) libraries. Its full functionality requires Python 2.0+ headers, but if these are not already installed, they can be omitted for the purposes of Texada. 

Once SPOT is extracted, navigate to that folder and run the commands

./configure (or ./configure --disable-python if Python is not installed)
make
make check
make install

to install.

TODO: add installation instruction for other OSs if possible

### Cloning project

An installation of mercurial is required. On *nix machines, sudo apt-get install mercurial should be sufficient. If using Eclipse, get the [MercurialEclipse](http://mercurial.selenic.com/wiki/MercurialEclipse) plug-in.

Create a [Bitbucket account](https://bitbucket.org/) and navigate to the [Texada code base](https://bitbucket.org/bestchai/texada). Clicking on "Clone" will give you the correct terminal command to clone, something like:
hg clone https://yourusername@bitbucket.org/bestchai/texada

From there, you can either run this command directly from terminal whilst in the directory you wish to clone to, or go from Eclipse. 

To clone from Eclipse run File->Import->Mercurial->Clone From Existing Mercurial Repository to import the project to your workspace. This process is detailed in the above link to MercurialEclipse.

### Building the project

In the top-level Texada directory, where the makefile exists, create a file called uservars.mk. In this file, provide the correct values for the following four variables:

SPOT_LIB: the location of the spot library
SPOT_INCL: the location of pot header files 
GTEST\_LIB: the location of gtest and gtest_main libraries
GTEST_INCL: the location of gtest header files

For example, uservars.mk might look like

      # User-Specific Variables
      # Specify path to SPOT library
      SPOT_LIB:=/path/to/libspot.a/
      # Specify path to GTest Libraries
      GTEST_LIB:=/path/to/libgtest.a/
      # Specify path to SPOT headers
      SPOT_INCL:=/path/to/spot/headers/
      # Specify path to GTest headers
      GTEST_INCL:=/path/to/gtest/headers/*

with all dummy paths replaced by real paths. SPOT\_LIB will probably point to pathtospot/spot/src/.libs/ if that is where libspot.a is. On a ubuntu machine, SPOT\_INCL will likely point to /usr/local/include/spot. The GTest libraries will be located wherever you build GTest and the GTest headers should be in pathtogtest/gtest/include (GTEST_INCL should point there). 

If building from shell, simply type the *make* command in the top-level directory.

If building from Eclipse, right-click on the Project. Follow Properties->C/C++Build. In Builder Settings, disable "Generate Makefiles automatically" and change Build Location to the Texada project. This should be ${workspace_loc:/Texada}, but can be navigated to via clicking the Workspace... option and selecting the Texada project. To build, press ctrl/cmd-b or right-click on the project and click "Build Project"