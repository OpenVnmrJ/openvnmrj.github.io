---
layout: article
title: Building OVJ on OS X
excerpt: "Building OVJ on OS X."
permalink: building-on-osx.html
---
## Building OVJ on OS X

This has been tested using gcc5.2 from https://github.com/timburrow/gcc-5.2-OSX.

If you just want to use openVnmrJ on OS X, please just download and install the pre-built package. Only those interested in modifying or exploring the core of VnmrJ need to down and build from source.

If you want to change macros, UI or pulse sequences, see the relevent README.

### To build from source:

1. Install Xcode 7 for OS X 10.10.5 Yosemite or OS X10.11 El Capitan or Xcode 6 on OS X 10.9.5 Mavericks from https://itunes.apple.com/app/xcode/id497799835 or http://developer.apple.com/
1. Install javaformac.dmg available at https://support.apple.com/kb/DL1573
  a. This might overwrite a newer copy of Java in /usr/bin/
  b. I have not tested this with a newer version of Java (like Java 8)
2. Download and install SConstruct from <a href='http://scons.org/download.php'>Scons.org</a>:
  ```
  curl -sO 'http://prdownloads.sourceforge.net/scons/scons-2.4.0.tar.gz'
  tar -xzvf scons-2.4.0.tar.gz
  cd scons-2.4.0
  sudo python setup.py install
  ```

3. Download and install gcc and gfortran
curl -O https://github.com/timburrow/gcc-5.2-OSX/releases/download/1.0/gcc5.2-osx-usrlocal.tar.bz2
sudo tar jxf gcc5.2-osx-usrlocal.tar.bz2 -C /
  a. This will be replaced by gcc4.9 in /vnmr/gcc later (since Linux version uses gcc 4.9); need to include a Darwin scons file

4. Set up the build environment

```
export PATH=/usr/local/bin:${PATH} # if not on path already
export JAVA_HOME=/Library/Java/JavaVirtualMachines/1.6.0.jdk/Contents/Home
# Make vjbudatastaionild directory and put ovj into it
mkdir ~/Documents/vjbuild
cd ~/Documents/vjbuild/ 
unzip ovj5.zip
unzip ovjtools4.zip
cd ovjTools
# Link to the java in ovjTools (remove the java link already present)
rm java
ln -s /Library/Java/JavaVirtualMachines/1.6.0.jdk .
cd ..; mkdir bin; cd bin
cp -a ../git-repo/src/scripts/makeovj .
cp -a ./git-repo/src/scripts/buildovj .
# patch git-repo/src/DOSY/SConstruct.dosy and git-repo/src/vnmrbg/SConstruct
# TODO SConstruct.dosy comment out link to libg2c
# TODO vnmrbg/SConstruct remove -rdynamic at link stage

# Edit buildovj to point to the reight directory
./buildovj
```
 
 5. If the build is successful, dvdimageOVJ will have:
 
 ```
 ls -l dvdimageOVJ/
total 0
drwxr-xr-x  3 timburrow  staff  102  5 Oct 10:21 Package_contents
drwxr-xr-x  4 timburrow  staff  136  5 Oct 10:21 install_resources
```
 
## Watchouts
 
 1. Some solidspack pulse sequences are different in case only; some macros and .c and .xml files will be overwritten when expanding the zip archive. Use a *case-sensitive* volume when using an HFS disk.

## Build OVJ

Building OVJ on OS X (El Capitan)

This is the buildovj file I used

```datastation

#! /bin/sh
#
#  Script to build an OVJ release.
#  Make a directory and put this file (buildovj) and the makeovj
#  script in a bin subdirectory
#  Set the following 2 global parameters.
#  ovjBuildDir defines where the git-repo will be built.
#  workspacedir used by ovjdvd and defines where the DVD images will be built.
#  dvdBuildName1 defines the name of the OVJ image
#  dvdBuildName2 defines the name of the MI image
#  dvdCopyDir1 defines where a copy of the OpenVnmrJ DVD image will be put.
#  dvdCopyDir2 defines where a copy of the OpenVnmrJ MI DVD image will be put.
#  set cdBuildDir[1,2] to null string to avoid the final copy
#  dvdCopyName1 defines the name of the OVJ copy
#  dvdCopyName2 defines the name of the MI copy
#  buildOVJ specifies whether the OVJ DVD image will be made
#  buildOVJMI specifies whether the OVJMI DVD image will be made
#
#  set doScons=yes to run scons
#  set doScons=no to not run scons. This also avoids removing directories
#              and does not change the git repo.
#              Use this if you are just making a DVD from pre-built files
#  set doGitClone=yes to get a new repo.
#  set doGitClone=rebuild to do a new checkout of "src"
#  set doGitClone=pull to pull recent changes to the repo and do a new checkout of "src"
#  set doGitClone=no to leave the current repo alone
#  set mail_list to addresses to email status of the build
#  set gitUSER to user name and address for git repo.
#  ovjAppName is only used by mac version to name /Applications/ovjAppName
#  sconsJoption helps speed up the process. Typical value is #CPUs+1
#

ovjBuildDir=/Users/timburrow/Documents/vjbuild
workspacedir=$ovjBuildDir
OVJ_TOOLS=$ovjBuildDir/ovjTools

dvdCopyDir1=
dvdCopyDir1=
dvdCopyDir2=

shortDate=`date +%F`
dvdBuildName1=dvdimageOVJ
dvdBuildName2=dvdimageOVJMI
dvdCopyName1=OVJ_$shortDate
dvdCopyName2=OVJ_MI_$shortDate
ovjAppName=OpenVnmrJ_1.1.app
sconsJoption=2

doGitClone=no
gitUSER=$USER@130.27.97.223/export/swrepos/git-repo
doScons=yes
buildOVJ=yes
buildOVJMI=no

# Potential optional set of values
# doGitClone=rebuild
# doGitClone=pull
doGitClone=no
# mail_list="dan.iverson@agilent.com"
# gitUSER=dan@130.27.97.223/export/swrepos/git-repo
# doScons=no
# buildOVJ=no
# buildOVJMI=no
# ovjAppName=OpenVnmrJ.app
# sconsJoption=5

date=`date +%F_%T`
if [ ! -d $ovjBuildDir/logs ]
then
   mkdir -p $ovjBuildDir/logs
fi
ovjLogFile=$ovjBuildDir/logs/makeovj.$date
cd $ovjBuildDir
export ovjBuildDir workspacedir OVJ_TOOLS dvdCopyDir1 dvdCopyDir2 dvdBuildName1 dvdBuildName2 dvdCopyName1 dvdCopyName2 ovjLogFile doScons doGitClone mail_list gitUSER ovjAppName buildOVJ buildOVJMI sconsJoption
$ovjBuildDir/bin/makeovj > $ovjLogFile 2>&1

```
