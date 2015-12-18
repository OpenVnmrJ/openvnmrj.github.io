---
layout: article
title: VnmrJ to Be Made Freely Available as Open Source OpenVnmrJ
author: tim_burrow
modified:
categories: press_releases
excerpt:
tags: []
image:
  feature:
  teaser: 400x250.gif
  thumb:
date: 2015-12-18T14:02:45-05:00
---
_Posted on behalf of the Varian Open-Source Steering Group (VOSSG)._

With the closing of Agilent NMR in October 2014 many users expressed an interest in having the ability to maintain and develop VnmrJ software independently of Agilent, to fix bugs and to add features. In response to this interest, a group of about 20 of us, users and some remaining employees of Agilent, formed a group called VOSSG (the Varian Open-Source Steering Group) to develop a plan. Agilent agreed, and software manager Dan Iverson has put a great deal of work into making a new version of VnmrJ (which contains over 3 million lines of code) suitable for open-source release. This effort should be completed in January 2016 and complete details will be available then. For now we would just like to provide a progress report for Varian and Agilent users.

Our plan is to release a version of VnmrJ (named OpenVnmrJ) and its source code, under an open-source license, freely available to all Varian/Agilent users and to others. The software will be available through the GitHub web site, as with many other open-source projects. Compiled versions will be available that will run on Linux or OS X, and source code will allow users who wish to make their own changes to do so. The VOSSG will oversee changes to future versions on GitHub; the group will be open to those interested in participating in this process.


The exact composition of the new release will be finalized in January, but the new version contains essentially the entire contents of VnmrJ 4.2 for spectroscopy and imaging, to run on a Linux workstation. These include the C code for Vnmrbg, the Magical macros used by VnmrJ, its Java interface, the pulse programming software, and most of the pulse sequences normally included with VnmrJ releases. As with Agilent's VnmrJ 4.2, versions will be available for Direct-Drive instruments (VnmrS, DD2 and Propulse), Unity INOVA, and Mercury systems. The release will not include the underlying acquisition software that runs inside the NMR console and a few other selected parts. However, installation on a spectrometer currently running VnmrJ 4.2 will automatically incorporate the existing parts of VnmrJ 4.2 needed to provide a fully working update.


OpenVnmrJ will be owned by the University of Oregon, which has accepted it from Agilent into their Innovation Partnership Services (IPS) unit, thanks to the efforts of Michael Strain and the director of the IPS unit. Agilent will continue to own VnmrJ 4.2 and previous versions, and it will continue, for the time being, to make the existing VnmrJ available to Agilent owners through its service department.


We anticipate that there will be new uses for the OpenVnmrJ software, many of which are now unforeseen. The actual development of OpenVnmrJ or its potential spin-offs will be in the hands of its users. The open-source license should impose very few restrictions on either personal or commercial use of the software. In the open-source philosophy, we will be looking forward to any contribution from the VnmrJ community to improve OpenVnmrJ and we will make the process as easy as possible, open, and transparent. As a start, we have put some documentation on GitHub at [http://openvnmrj.org](http://openvnmrj.org).


If you have questions or ideas, feel free to contact any of the VOSSG members, whose names are included below. We hope that this release of OpenVnmrJ in January will be a small bright spot in what otherwise has been a dismal development for all of us this past year. We look forward to your ideas and to interesting discussions.

VOSSG members who are available to contact:  

-   Tim Burrow tim.burrow@utoronto.ca
-   Craig Butts craig.butts@bristol.ac.uk
-   Dan Iverson dan.iverson@agilent.com
-   Steve McKenna stephen.mckenna@ineos.com
-   Gareth A. Morris g.a.morris@manchester.ac.uk
-   Mathias Nilsson mathias.nilsson@manchester.ac.uk
-   Walt Niemczura walt@hawaii.edu
-   Eric Paulson eric.paulson@yale.edu
-   David Rice daverice@stanford.edu
-   John Ryan john_ryan@agilent.com
-   Michael Strain mstrain@uoregon.edu
