OpenVnmrJ
=========

README.ovj
v0.2
17 August 2015
Dan Iverson & John Ryan

BUILD REQUIREMENTS
==================

EL6 (RHEL/CentOS 6)
The minimum package requirement for EL6 assumes that your system was installed with the
"Software Development Workstation" package selection as required by VnmrJ.  This build
configuration has been tested on CentOS 6.6 but should work for any RHEL or CentOS 6.x.

`yum install compat-gcc-34-g77 glibc-devel.i686 libstdc++.i686 libX11-devel.i686 libXt-devel.i686 openmotif-devel.i686 scons`

Optionally, you can also install gsl-devel and libtiff-devel if you wish to compile using the GNU
scientific library.  Code compiled with the GSL will be subject to license restrictions.

Ubuntu Trusty Tahr 14.04 LTS
The minimum package requirement for Ubuntu Trusty Tahr 14.04 LTS assumes that you have
installed the standard desktop edition of Ubuntu.  This build configuration has been
tested on Ubuntu but should work for any *buntu Trusty Tahr 14.04 LTS distribution.

`sudo apt-get install fort77 g++ lib32stdc++-4.8-dev libc6-dev-i386 libmotif-dev:i386 libx11-dev:i386 libxt-dev:i386 scons`

Optionally, you can also install libgsl0-dev and libtiff5-dev if you wish to compile 
components using the GNU scientific library.  Code compiled with the GSL will be subject
to license restrictions.

Full package requirements including dependent packages are listed in the appendix of
this document.

INSTALLATION & COMPILATION
==========================

Make a directory. Lets call it ovj_build.  unzip the source code file inside that directory.
It will add a git-repo. The git-repo directory contains the following directories and files.
These files may be open-sourced.

SConstruct   This is the definition file used by scons. It is similar to Makefile used by
             the make command.
scripts      This contains tools used by scons.
src          This contains the source code for OpenVnmrJ. Some of these directories also
             contain a SConstruct file that is used to build / compile that specific
             program.

The ovjTools can be unzipped in the ovj_build directory or anyplace that you want to put it.
The ovjTools directory contains code from external sources. This code should not be
open-sourced by OpenVnmrJ. It contains the following directories. (In earlier edition,
this was the 3rdParty directory.

fftw           Used by xrecon (imaging program)
java           Used by all java programs. It is a soft link to the java jdk.
JavaPackages   Used by vjmol and vnmrj
jdk1.6.0_39_64 Java jdk.
JMF-2.1.1e     Used by vnmrj (simplemovie.jar)
junit          Used by apt, probeid, and vjclient
NDDS           Used by nvlocki, nvexpproc, nvinfoproc, nvrecvproc, nvsendproc
tcl            This contains headers and libraries for compiling programs that
               require tcl (Roboproc)

To compile the java programs, the OVJ_TOOLS env parameter must be set to point to the
ovjTools directory. The ovjTools directory does not necessarily need to be in the same
directory as the git-repo directory, although that may be a convenient place. In a bash
shell, the command would be
  export OVJ_TOOLS=<path>
In a csh, the command would be
  setenv OVJ_TOOLS <path>
We compile VnmrJ java programs with jdk1.6.0_39_64. The java in ovjTools should be a soft link
to the actual java JDK. 

Change directory to git-repo and run the command "scons". It will use the SConstruct file
to  compile the programs in src and place the results in directories at the same level
as the git-repo level. The console directory will contain console-specific files.
The vnmr directory will contain files that are generic. The options directory contains
optional software and code that is used during installation.

You can also change into specific directories in src and run scons. That will build that
specific program. For example,

```
cd src/vnmrbg
scons
```

will build only the Vnmrbg program.  Note that this preliminary version of OpenVnmrJ has the
go, dps, and svf commands of Vnmrbg disabled.

The src directory has a number of subdirectories. In general, each subdirectory corresponds to one
or more programs that need to be compiled. Some of the subdirectories contain code that is shared
by several programs. The src directory contains the following subdirectories.
```
3D          Code for compressfid, ft3d, getplane
acqproc     Shared files
aip         Shared files used by vnmrbg. (aip -> advanced image processing)
Asp         Shared files used by vnmrbg. (Asp -> advanced spectral processing)
atproc      Code for Atproc
ddl         Shared files
expproc     Expproc for Inova and Mercury
ib          Shared files (image browser)
infoproc    Infoproc for Inova and Mercury
kpsg        PSG for Mercury
magic       Shared files
masproc     Masproc for Inova
nacqi       Shared files
nautoproc   Autoproc
ncomm       Shared files and acqproc and ncomm libraries.
nvacq       Shared files with DDR console software
nvexpproc   Expproc for DDR systems
nvinfoproc  Infoproc for DDR systems
nvpsg       PSG for DDR systems
nvrecvproc  Recvproc for DDR systems
nvsendproc  Sendproc for DDR systems
procproc    Procproc
psg         PSG for Inova
psglib      Pulse sequences shared by Inova and DDR
recvproc    Recvproc for Inova and Mercury systems
roboproc    Roboproc
sendproc    Sendproc for Inova and Mercury systems
stat        Code for Infostat and showstat
vnmr        Shared files
vnmrbg      Code for Vnmrbg
vnmrj       Currently shared files
vobj        Shared files
vwacq       Shared files with Inova console software
xracq       Shared files with VXR console software
```
New since last version:
```
admin       VnmrJ installer java program 
apt         Auto ProTune java program
aslmirtime  Imaging program (requires GPL license)
autotest    Autotest appdir
bin         Compiled programs in /vnmr/bin
bin_image   Compiled imaging programs in /vnmr/bin (requires GPL license)
biopack     Biopack appdir
biosolidspack Biosolidspack appdir
bootpd.rh51 Bootp program for Inova and Mercury
common      This contains text files that do not need further processing / compiling,
            including CRAFT.
cryo        Cryobay communications java program
cryomon     Cryo monitor communications java program
ddr         Protocols for DDR
DOSY        DOSY files
Gilson      VAST files
gxyzshim    3D gradient shimming
IMAGE       Files for imaging
inova       Files to support Inova
ipsglib     Inova specific pulse sequences
jaccount    Accounting program
jplot       jplot program
kpsg        PSG for Mercury
kpsglib     Pulse sequences for Mercury
languages   Support for Chinese and Japanese
layouts     layout XML files
LCNMR       LC-NMR files
lcpeaks     LC peak analysis tool
managedb    Program used by Locator and dbsetup
mercury     Files to support Mercury
nvpsglib    DDR specific pulse sequences
p11         Files for Part 11 option
probeid     probeid communications program
scripts     Scripts in /vnmr/bin (and other scripts used for install, etc)
solidspack  Solidspack appdir
tcl         tcl scripts (autotest, etc)
veripulse   veripulse appdir
vjclient    Program used by probeid
vjmol       Auxiliary java program to connect jmol with vnmrj
web         Programs to support tablet
vnmrj       vnmrj java program (requires GPL license)
xrecon      Imaging reconstruction program (requires GPL license)
```

APPENDIX
========

EL6 (RHEL/CentOS 6)
Full list of required packages for EL 6 starting from a "Software Development Workstation"
configuration:
```
compat-gcc-34
compat-gcc-34-g77
compat-libf2c-34
expat.i686
fontconfig.i686
freetype.i686
glibc.i686
glibc-devel.i686
libgcc.i686
libICE.i686
libjpeg-turbo.i686
libpng.i686
libstdc++.i686
libSM.i686
libuuid.i686
libX11.i686
libX11-devel.i686
libXau.i686
libxcb.i686
libXext.i686
libXft.i686
libXmu.i686
libXp.i686
libXrender.i686
libXt.i686
libXt-devel.i686
nss-softokn-freebl.i686
openmotif.i686
openmotif-devel.i686
scons
zlib.i686  
```
And optionally:
```
gsl
gsl-devel
libtiff-devel
```
Ubuntu Trusty Tahr 14.04 LTS
Full list of required packages for Ubuntu Trusty Tahr 14.04 LTS starting from a standard
desktop edition installation:
```
f2c
fort77
g++
g++-4.8
gcc-4.8-multilib
gcc-4.9-base:i386
gcc-multilib
lib32asan0
lib32atomic1
lib32gcc-4.8-dev
lib32gcc1
lib32gomp1
lib32itm1
lib32quadmath0
lib32stdc++-4.8-dev
lib32stdc++6
libc6-dev-i386
libc6-dev-x32
libc6-i386
libc6-x32
libc6:i386
libexpat1:i386
libf2c2
libf2c2-dev
libfontconfig1:i386
libfreetype6:i386
libgcc1:i386
libice-dev:i386
libice6:i386
libjpeg-turbo8:i386
libjpeg8:i386
libmotif-common
libmotif-dev:i386
libmrm4
libmrm4:i386
libpng12-0:i386
libpthread-stubs0-dev:i386
libsm-dev:i386
libsm6:i386
libstdc++-4.8-dev
libuil4
libuil4:i386
libuuid1:i386
libx11-6:i386
libx11-dev:i386
libx11-doc
libx32asan0
libx32atomic1
libx32gcc-4.8-dev
libx32gcc1
libx32gomp1
libx32itm1
libx32quadmath0
libxau-dev:i386
libxau6:i386
libxcb1-dev:i386
libxcb1:i386
libxdmcp-dev:i386
libxdmcp6:i386
libxext6:i386
libxft2:i386
libxm4
libxm4:i386
libxmu6:i386
libxrender1:i386
libxt-dev:i386
libxt6:i386
scons
uil
x11proto-core-dev
x11proto-input-dev
x11proto-kb-dev
xorg-sgml-doctools
xtrans-dev
zlib1g:i386
```
And optionally:
```
libgsl0-dev
libgsl0ldbl
libjbig-dev
libjpeg-dev
libjpeg-turbo8-dev
libjpeg8-dev
liblzma-dev
libtiff5-dev
libtiffxx5
zlib1g-dev
```