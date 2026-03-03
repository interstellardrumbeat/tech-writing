# How to play your drum set with eDrumIn and Superior Drummer 3 on Debian

## Table of Contents  
- [Glossary](#glossary)
- [Introduction](#introduction)
- [Installation types](#installation-types)
- [System requirements](#system-requirements)
- [SETUP 1 - SD3 bridged to Linux DAW](#setup-1---sd3-bridged-to-linux-daw)
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

The eDrumIn+SD3 setup on Debian can be used following different installation routes and setups (i.e. different bridges, software, audio drivers, DAWs, etc...). I have tested 3 ways, of which only one gives me the results I need and has proven effective. For completeness I will report a list of all the options, including the untested ones. 

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
- **RAM**: minimum 4 GB (8 GB recommended)
- **External AUDIO card/interface**: for minimal latency (integrated AUDIO card don't work well)

## SETUP 1 - SD3 bridged to Linux DAW

The main features of this setup are:
- eDrumIn on Linux
- SD3 in Wine
- yabridge on Linux and used to bridge SD3 from Wine to Linux
- Reaper (or any other DAW you like) on Linux
- eDrumIn+SD3 operated through the DAW
- SD3 can be personalized in Wine

### Step 1 - Install eDrumIn

Download and install the eDrumIn interface at the following link:  
[eDrumIn official website](https://www.audiofront.net/downloads.php)

### Step 2 - Install Wine

SD3 operates on 64-bit architecture. Before proceeding, verify the architecture of your PC with:
```
dpkg --print-architecture
dpkg --print-foreign-architectures
```
The first command should give "amd64" the second "i386". 
If no "i386" gets displayed, run `sudo dpkg --add-architecture i386 && sudo apt update` and verify again with `dpkg --print-foreign-architectures`.

Proceed to complete install with:
```
sudo apt install \
      wine \
      wine32 \
      wine64 \
      libwine \
      libwine:i386 \
      fonts-wine \
      winetricks
```

### Step 3 - Setup Wine

Once installed, proceed with the creation and configuration of the wine prefix (the virtual Windows environment), running the following command in the terminal:
```
WINEPREFIX=~/wine-sd3 winecfg 
```

The name for the prefix can be anything you want. I use _wine-sd3_, since I have multiple dedicated prefixes.  
`winecfg` will open the prefix configuration GUI. Check for if the selected OS is Windows 10 (or 11). If not change it and then close the GUI.

### Step 4 - Install SD3

#### 4.1. Install SD3 in your wine prefix

Download the [Toontrack Product Manager](https://www.toontrack.com/product-manager/) and install it in the Wine prefix you have previously created, as follows (you might need to rename the exe):
```
wine-sd3 ToontrackProductManagerInstaller.exe
```

This operation will require some time since it will trigger the installation of all the required .NET dependencies. 
Once completed, open the Toontrack Product Manager and proceed with the installation of SD3.
>TIP: To minimize the time for the setup I suggest doing the minimal install, i.e. only the software and the main libraries. In this way, you have wasted less time in case something goes wrong and you have to delete the wine prefix restarting from zero.

#### 4.2. Check the VST folder

Since it will be need for yabridge, verify that SD3 has been correctly installed.
The folder should be somewhere like:
```
~/wine-sd3/drive_c/Program Files/Common Files/VST3/
```
and it should contain `Superior Drummer 3.vst3`.

### Step 5 - Install and Configure Yabridge 

#### 5.1. Install Yabridge

Yabridge can be easily installed following the instructions on the corresponding [GitHub repo](https://github.com/robbert-vdh/yabridge). 
For the sake of simplicity I will add here the section of the original Yabridge README dedicated to Debian.

>1. First download the latest version of yabridge from the [releases
        page](https://github.com/robbert-vdh/yabridge/releases). These binaries
        currently target Ubuntu 20.04, and should work on any other distro
        that's newer than that.
>2. Extract the contents of the downloaded archive to `~/.local/share`, such
        that the file `~/.local/share/yabridge/yabridgectl` exists after
        extracting. You can extract an archive here from the command line with
        `tar -C ~/.local/share -xavf yabridge-x.y.z.tar.gz`. If you're
        extracting the archive using a GUI file manager or archive tool, then
        make sure that hidden files and directories are visible by pressing
        <kbd>Ctrl+H</kbd>. You should also double check that your archive
        extraction tool didn't create an additional subdirectory in
        `~/.local/share`. Dragging and dropping the `yabridge` directory from
        the archive directly to `~/.local/share` is the best way to make sure
        this doesn't happen.
>3. **Whenever any step after this mentions running `yabridgectl <something>`,
        then you should run `~/.local/share/yabridge/yabridgectl <something>`
        instead.**

For easier use, you can add yabridge to your PATH with (check and edit with your correct path):
```
export PATH="$HOME/.local/share/yabridge:$PATH"
```

#### 5.2. Register your VST folder in Yabridge

Using the path of the VST folder in your wine prefix from Step 4.2, tell yabridge where to find the installed VST:
```
yabridgectl add "$HOME/wine-sd3/drive_c/Program Files/Common Files/VST3"
```
synchronize with:
```
yabridgectl sync
```
and verify the correct registration by checking if there the `~/.vst3/yabridge/` folder has been created.

### Step 6 - Install Reaper (or any other DAW of your choice)

If you go for Reaper, download it and install it from [here](https://www.reaper.fm/download.php).

Instructions for installation are given on the readme inside the downloaded .tar.xz file, but it's pretty straightforward: first make the `./install_reaper.sh` script executable with the usual `sudo chmod +x /path/install-reaper.sh` command, then run it from the terminal.   

### Step 7 - Install and configure PipeWire-JACK

#### 7.1. Install PipeWire-JACK

Before configuring Reaper, we need a powerful native AUDIO-driver, such as PipeWire-JACK, which works well with an external audio card for minimal latency.

Install it with:
```
sudo apt install pipewire-audio pipewire-jack qpwgraph
systemctl --user restart pipewire pipewire-pulse
```
and launch `qpwgraph` to verify that you external audio device is recognised. 

#### 7.2. Configure for minimal audio latency

Create or edit:
```
~/.config/pipewire/pipewire.conf.d/99-lowlatency.conf
```
and add:
```
context.properties = {
    default.clock.rate          = 48000
    default.clock.quantum       = 64
    default.clock.min-quantum   = 32
    default.clock.max-quantum   = 128
}
```

This will set the buffer to 64 samples, which is perfect to play.

>IMPORTANT: If your audio device does not support 64 samples, you need to set up the buffer to 128 otherwise you might encounter audio distortion when playing. See [Troubleshooting](#troubleshooting) for details.

### Step 8 - Run and configure Reaper

Run reaper plus JACK audio driver through terminal, as follows:
```
pw-jack reaper
```

This forces Reaper to run using the PipeWire-JACK audio driver. In my case, running Reaper in any other way, would cause it to being unable to find the correct driver and give an error. See [Troubleshooting](#troubleshooting) for details.

#### X.1. Load eDrumIn in Reaper

#### X.2. Load SD3 in Reaper

#### X.3. Play

## Post installation

### Configuration options

## Troubleshooting

To edit later. Temporary notes:
1) wineHQ instead of standard wine;
2) audio distortion (64 vs 128 samples)
3) Reaper does not fine JACK audio drivers and gives an error
