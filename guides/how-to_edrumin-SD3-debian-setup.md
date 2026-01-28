# How effectively play your drum set with eDrumIn and Superior Drummer 3 on Debian

## Table of Contents  
- [Glossary](#glossary)
- [Introduction](#introduction)
- [Installation types](#installation-types)
- [System requirements](#system-requirements)
- [Before you begin](#before-you-begin)
- [OPTION 1 - SD3 bridged to Linux DAW](#setup-1---sd3-bridged-to-linux-daw)
- [Post installation](#post-installation)
- [Troubleshooting](#troubleshooting)

## Glossary

- VST = Virtual Studio Technology
- DAW = Digital Audio Workstation
- eDrumIn = hardware, a MIDI interface used to connect the drum kit to the PC
- Superior Drummer 3 (SD3) = a VST, used to convert MIDI inputs in drums sounds
- Module = a MIDI interface with VST integrated in one single hardware piece
- Wine = compatibility layer, allows users to run Windows applications on Linux

## Introduction

This guide is born primarily from a need I have at least once per year, since I often format my PC. Every time, I end up trying to trace back all the steps required to install all the necessary libraries, software, etc...to finally play my electronic drum kit with the MIDI interface **eDrumIn** and the VST **Superior Drummer 3 (SD3)** on Debian (currently 13, Trixie). 

## Installation types

The eDrumIn+SD3 setup on Debian can be used following different installation routes and setups (i.e. different bridges, software, sound drivers, DAWs, etc...). I have tested 3 ways, of which only one gives me the results I need and has proven effective. For completeness I will report a list of all the options, including the untested ones. 

NOTE: the main limitation comes from SD3, which does not have a Linux version and must be always installed in Wine. This will be the common factor to the different installation paths.
From there, it all comes down to "where you want to install eDrumIn and how you want to use SD3 (directly in Wine or bridge to Linux)".

| | **Setup** | **Description** | **How-to** |
|----| --------- | ------------- | ----------- |
| 1. | eDrumIn (Linux) + SD3 (wine) + yabridge (Linux) + DAW (Linux, e.g. Reaper) | SD3 bridged to Linux and operated through a DAW (e.g. Reaper), except for small tweaks done directly in wine (i.e. personalize the kit with the original SD3 GUI) | [Link to section](#setup-1---sd3-bridged-to-linux-daw) |
| 2. | eDrumIn (Linux) + Pipewire-Jack (Linux) + SD3 (wine) + WineASIO (wine) | SD3 used without any DAW, directly in wine (as if in Windows) with the original fully working GUI | [Link to section](#) |
| 3. | eDrumIn (Linux) + SD3 (wine) + yabridge (Linux) + Pipewire-Jack (Linux) + Carla (Linux) | SD3 bridged to Linux and operated through a Carla, except for small tweaks done directly in wine (i.e. personalize the kit with the original SD3 GUI) | [Link to section](#) |

## System requirements

The main requirements derive from SD3. 
- **FREE DISK SPACE**:
    - _Minimum install_ - 100 GB (basic sound library download and installation space, plus other software)
    - _Complete install_ - 325 GB (full sound library download and installation space, plus other software)
- **RAM**: 4 GB (8 GB recommended)

## Before you begin

## SETUP 1 - SD3 bridged to Linux DAW

This setup is the only stable one I managed to setup.

The main features are:
- eDrumIn on Linux
- SD3 on Wine
- yabridge on Linux and used to bridge SD3 from Wine to Linux
- Reaper (or any other DAW you like) on Linux
- eDrumIn+SD3 operated through the DAW

### Step 1 - Install eDrumIn

Download and install the eDrumIn interface at the following link:  
[eDrumIn official website](https://www.audiofront.net/downloads.php)

### Step 2 - Install Wine

### Step 3 - Install SD3 in Wine

### Step 4 - Install yabridge

### Step 5 - Install Reaper

### Step 6 - Install PipeWire-JACK (recommended)

### Step 7 - Setup Reaper

#### 7.1. Load SD3 and eDrumIn in Reaper

#### 7.2. Configure audio for low-latency

#### 7.3. Play

## Post installation

### Configuration options

## Troubleshooting
