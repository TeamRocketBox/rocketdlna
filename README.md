# RocketDLNA project

This project is a fork of the [MiniDLNA project](http://sourceforge.net/projects/minidlna/).

The original Copyright holders of MiniDLNA are

- (c) 2009 Justin Maggard
- (c) 2006-2007 Thomas Bernard


This directory contains the RocketDLNA daemon software.
This software is subject to the conditions detailed in
the LICENCE file provided with this distribution.

Parts of the software including the discovery code are
licensed under the BSD revised license which is detailed
in the LICENSE.miniupnpd file provided with the distribution.
More information on MiniUPnPd can be found at http://miniupnp.free.fr.


The RocketDLNA daemon is an UPnP-A/V and DLNA service which
serves multimedia content to compatible clients on the network.
See http://www.upnp.org/ for more details on UPnP
and http://www.dlna.org/ for mode details on DLNA.

## Prerequisites

- libexif
- libjpeg
- libid3tag
- libFLAC
- libvorbis
- libsqlite3
- libavformat (the ffmpeg libraries)

## Goals

Due to the fact I am a fan of CMake and C++ this project will somehow be transferred to CMake and C++ in the future.

- Add CMake support
- Rename the daemon from minidlna to rocketdlan
- Modernize the code with the help of C++17

-
