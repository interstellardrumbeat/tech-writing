# How effectively play your drum set with eDrumIn and Superior Drummer 3 on Debian

## Glossary

* VST = Virtual Studio Technology  
* DAW = Digital Audio Workstation  

## Introduction

Playing electronic drum kits at home can be **painful** if you, like me, don't like buying and playing basic kits with pre-assembled modules, but prefer to complicate your life to get a better (and personalized) playing experience. 
Of course, this path becomes even more complicated if you do not use Windows as your main OS. 

This guide is born primarily from a need I have at least once per year, since I often format my PC. Every time, I end up trying to trace back all the steps required to install all the necessary libraries, software, etc...to finally play my electronic drum kit with the MIDI interface **eDrumIn** and the VST **Superior Drummer 3 (SD3)** on Debian (currently 13, Trixie). 

## Installation types

The eDrumIn+SD3 setup on Debian can be used following different installation routes and setups (i.e. different bridges, software, sound drivers, DAWs, etc...). I have tested 3 ways, of which only one gives me the results I need and has proven effective. For completeness I will report a list of all the options, including the untested ones. 

NOTE: the main limitation comes from SD3, which does not have a Linux version and must be always installed in Wine. This will be the common factor to the different installation paths.
From there, it all comes down to "where you want to install eDrumIn and how you want to use SD3 (directly in Wine or bridge to Linux)".

| | **Setup** | **Description** | **How-to** |
|----| --------- | ------------- | ----------- |
| 1. | eDrumIn (Linux) + SD3 (wine) + yabridge (Linux) + DAW (Linux, e.g. Reaper) | SD3 bridged to Linux and operated through a DAW (e.g. Reaper), except for small tweaks done directly in wine (i.e. personalize the kit with the original SD3 GUI) | [Link to section](#) |
| 2. | eDrumIn (Linux) + Pipewire-Jack (Linux) + SD3 (wine) + WineASIO (wine) | SD3 used without any DAW, directly in wine (as if in Windows) with the original fully working GUI | [Link to section](#) |
| 3. | eDrumIn (Linux) + SD3 (wine) + yabridge (Linux) + Pipewire-Jack (Linux) + Carla (Linux) | SD3 bridged to Linux and operated through a Carla, except for small tweaks done directly in wine (i.e. personalize the kit with the original SD3 GUI) | [Link to section](#) |

## Acknowledgment

This guide is written following a template provided by [the Good Docs Project](https://www.thegooddocsproject.dev) and the [Diátaxis](https://diataxis.fr) framework.
