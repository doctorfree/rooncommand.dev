---
title: Voice Activated Roon Control
author: doctorfree
date: 2023-08-03 13:42:00 +0800
categories: [Blogging, Tutorial, Information]
tags: [info voice control]
pin: true
img_path: "/posts/20230803"
---

## Overview

Several users have posted in the Roon forums various ways to use Apple Siri to
control Roon. These usually take the form of a fake device in HomeBridge that
then communicates with HomeKit and Siri. This seemed cool but maybe overkill.
I was able to get Siri voice control of Roon working with simple SSH shortcuts
that execute Python scripts which utilize the Roon API to control Roon.

Subsequently I activated and configured the MMM-GoogleAssistant and MMM-Detector
modules on my MagicMirror and wrote recipes to control Roon using Google Assistant.

Both of these methods, Siri voice control of Roon and Google Assistant voice
control of Roon, utilize a command line interface that issues commands to the
Roon Core. With Siri the shell command is executed using SSH and with Google
Assistant the shell command is executed by a MagicMirror module without the
need for SSH.

I will describe in detail both of these methods for voice control of Roon and
the setup precedures required for each. Both methods consist of getting a
voice assistant working then creating voice triggers in that assistant that
activate a corresponding action which executes a RoonCommandLine command.

First I will address the voice assistant setup for each. Following those sections
I will describe the integration of the RoonCommandLine package into the setup
and provide example configurations.

## Table of Contents

1. [Using Apple Siri](#using-apple-siri)
1. [Using Google Assistant](#using-google-assistant)
   1. [Google Assistant Requirements](#google-assistant-requirements)
   1. [Google Assistant Setup](#google-assistant-setup)
   1. [Google Assistant Roon Control Setup](#google-assistant-roon-control-setup)
1. [RoonCommandLine Setup](#rooncommandline-setup)
   1. [RoonCommandLine Requirements](#rooncommandline-requirements)
   1. [RoonCommandLine Installation](#rooncommandline-installation)
      1. [Debian Package installation](#debian-package-installation)
      1. [RPM Package installation](#rpm-package-installation)
      1. [Mac OS X installation](#mac-os-x-installation)
      1. [Post installation configuration](#post-installation-configuration)
         1. [Zone groupings and defaults](#zone-groupings-and-defaults)
1. [Apple Siri Roon Control Setup](#apple-siri-roon-control-setup)
1. [References](#references)
   1. [SSH Setup for Apple Shortcuts](#ssh-setup-for-apple-shortcuts)
   1. [MagicMirror Google Assistant Setup](#magicmirror-google-assistant-setup)

## Using Apple Siri

Apple SSH shortcuts can be used to execute commands on systems that allow
SSH access. I used an Ubuntu 20.10 system recently installed to install the
Python Roon API project (pip install roonapi) and quickly cobbled together a
Python script based on one of the examples in that project. The Python script
accepts an argument specifying an artist name in my Roon library. It then uses
the Roon API to play music from my library by that artist in the specified zone.

On my iPhone I then created shortcuts which use the “Run script over SSH”
option for Apple Scripting shortcuts. The shortcuts execute a Bash command
which is a shell script that executes the Python script with appropriate
arguments. It all seemed to work. Over time I refined this setup to utilize
the `roon` frontend to the Python Roon API and added shortcuts for a variety
of Roon commands and control.

To get started with Apple SSH shortcuts first enable SSH access on the system
where the [RoonCommandLine](https://github.com/doctorfree/RoonCommandLine)
package will be installed. Follow one of the many guides for setting up SSH
with Apple Shortcuts. For example, these two guides should get you started:

- [Remote control your Mac with your iPhone and SSH Key Shortcuts](https://dougbeal.com/2019/11/02/remote-control-your-mac-with-your-iphone-and-ssh-key-shortcuts/)
- [Setting up SSH for Shortcuts](https://www.thoughtasylum.com/2020/06/01/setting-up-ssh-for-shortcuts/)

Verify that Apple Siri is working and responds to queries like "Hey Siri", "What time is it?". Verify that SSH Shortcuts are working by creating a shortcut that performs
a simple command like `ping` as described in the guides above. Once Siri and
SSH Shortcuts are confirmed to be working, proceed to the
[RoonCommandLine Setup](#rooncommandline-setup)
described below followed by the
[Apple Siri Roon Control Setup](#apple-siri-roon-control-setup).

See the wiki article
[Roon Voice Commands with Siri](https://github.com/doctorfree/RoonCommandLine/-/wikis/Roon-Voice-Commands-with-Siri)
for a detailed walkthru of Roon voice control using Siri and Apple Shortcuts.

## Using Google Assistant

See the wiki article
[Roon Voice Commands with Google Assistant](https://github.com/doctorfree/RoonCommandLine/-/wikis/Roon-Voice-Commands-with-GA)
for a detailed walkthru of Roon voice control using MagicMirror modules and
Google Assistant.

### Google Assistant Requirements

This method for voice control of Roon requires a
[MagicMirror](https://magicmirror.builders/) with the
[MMM-GoogleAssistant wiki](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
and [MMM-Detector wiki](http://wiki.bugsounet.fr/en/MMM-Detector) modules
activated and configured properly. Setup for this method is considerably
more difficult but once accomplished results in a superior quality setup
with far more ease and flexibility of use. The Siri setup requires SSH and
the Apple Shortcuts are more difficult to setup and maintain than the
Google Assistant voice recipes.

The Google Assistant setup requires a MagicMirror - something
I am guessing most people do not have. However, the MagicMirror is super
cool so set one up then use this Roon voice control method :smiley:
To get started with a MagicMirror installation, see the
[MagicMirror Documentation](https://docs.magicmirror.builders/).
Alternately, and preferably, install the
[MirrorCommand package](https://github.com/doctorfree/MirrorCommand)
which performs an automated installation and configuration of MagicMirror
along with required modules.

### Google Assistant Setup

If you have a MagicMirror with a microphone then you can setup Google Assistant
by following the instructions at the
[MMM-GoogleAssistant wiki](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant).
This setup is not simple as it requires a Google Project with Actions and OAuth
credentials. However, I found this 12 year old girl on YouTube who did it and
so I figured I could too. It turns out I could so you probably can too.

MMM-GoogleAssistant requires MMM-Detector which can also be setup and configured
following the instructins at the
[MMM-Detector wiki](http://wiki.bugsounet.fr/en/MMM-Detector).

### Google Assistant Roon Control Setup

After activating and configuring MMM-GoogleAssistant and MMM-Detector it is now
time to tackle setting up Roon control with Google Assistant. Test the initial
MMM-GoogleAssistant setup by saying something like "Hey Google" or "OK Google"
or "Computer" or whatever your MMM-Detector "Model" setting is. MMM-Detector
should wake up and listen. Then say something like "What time is it" and verify
that you get a response from Google Assistant. It it's working we can proceed.

## RoonCommandLine Setup

Voice control of Roon as described in this document requires the
use of a command line interface to issue the Roon commands. This is
accomplished with the
[RoonCommandLine](https://github.com/doctorfree/RoonCommandLine)
package which contains a shell command that acts as a frontend to
the [Python Roon API](https://github.com/pavoni/pyroon).

See the
[RoonCommandLine README](https://github.com/doctorfree/RoonCommandLine/-/blob/master/README.md)
for an overview of this package and documentation on its installation,
configuration, and use.

### RoonCommandLine Requirements

RoonCommandLine can be installed on either Linux or Mac OS X systems.
It requires a [Roon Core System](https://roonlabs.com/) reachable on the
local network, [Bash](<https://en.wikipedia.org/wiki/Bash_(Unix_shell)>),
[Python 3](https://www.python.org/), and the
[Python Roon API](https://github.com/pavoni/pyroon). The Python Roon API
will be installed as part of the RoonCommandLine installation process.

Ensure that a Roon Core System is running on the local area network and
Python 3 is installed on the Linux or Mac on which you wish to install
the RoonCommandLine package. Most modern Linux systems will have Python 3
already installed. A good guide for installing Python 3 on Mac OS X can
be found at <https://docs.python-guide.org/starting/install3/osx/>

### RoonCommandLine Installation

RoonCommandLine v2.0.0 and later can be installed on Linux systems using
either the Debian packaging format or the Red Hat Package Manager (RPM).
Support is also included for installing on Mac OS X. Other systems will
require a manual installation described below. The Mac OS X installation
procedure may also work under Microsoft's Windows Subsystem for Linux but
it is as yet untested.

#### Debian Package installation

Many Linux distributions, most notably Ubuntu and its derivatives, use the
Debian packaging system.

To tell if a Linux system is Debian based it is usually sufficient to
check for the existence of the file `/etc/debian_version` and/or examine the
contents of the file `/etc/os-release`.

To install on a Debian based Linux system, download the latest Debian format
package from the
[RoonCommandLine Releases](https://github.com/doctorfree/RoonCommandLine/-/releases).

Install the RoonCommandLine package by executing the command

```bash
sudo apt install ./RoonCommandLine_<version>-<release>.deb
```

or

```console
sudo dpkg -i ./RoonCommandLine_<version>-<release>.deb
```

#### RPM Package installation

Red Hat Linux, SUSE Linux, and their derivatives use the RPM packaging
format. RPM based Linux distributions include Fedora, AlmaLinux, CentOS,
openSUSE, OpenMandriva, Mandrake Linux, Red Hat Linux, and Oracle Linux.

To install on an RPM based Linux system, download the latest RPM format
package from the
[RoonCommandLine Releases](https://github.com/doctorfree/RoonCommandLine/-/releases).

Install the RoonCommandLine package by executing the command

```bash
sudo yum localinstall ./RoonCommandLine_<version>-<release>.rpm
```

or

```console
sudo rpm -i ./RoonCommandLine_<version>-<release>.rpm
```

#### Mac OS X installation

RoonCommandLine requires Python 3. See the excellent
[Hitchhiker's Guide to Python](https://docs.python-guide.org/starting/install3/osx/)
for step by step instructions to install Python 3 on Mac OS X. If you already
have `Homebrew` installed on your Mac then you can install Python 3 with:

`brew install python`

Once the Python 3 dependency is met, install RoonCommandLine by
cloning the RoonCommandLine repository and executing the `Install` script:

```bash
    git clone `https://github.com/doctorfree/RoonCommandLine.git`
    cd RoonCommandLine
    ./Install
```

**Note:** A cleaner installation can be accomplished by executing the `Install`
script as a user with `sudo` privileges and as the user which will be used
to SSH in to the system. If you are not going to enable SSH support, at least
make sure the user has sudo privileges.

#### Post installation configuration

Default settings are applied during the installation process. The primary area
of post-installation configuration is setting the ZONEGROUPS and DEFAULT values
in the file `/usr/local/Roon/etc/roon_api.ini`. The RoonCommandLine installation
attempts to automate this configuration and should have provided a good starting
point with default settings in `roon_api.ini` but you may wish to adjust these.

##### Zone groupings and defaults

In Roon, you can view your existing zones by visiting `Settings->Audio`. The names
of the enabled audio devices are your zones. You can change the name of a zone by
clicking the "pencil" icon next to the name in the Roon audio settings screen.

Modify `roon_api.ini` with your desired zone groupings and default values.
In particular, set the `DefaultZone` value in the DEFAULT section to a zone
that will be available, enabled, and one you wish to use as your primary
default fallback zone. The installation picked a DefaultZone for you and
you may be satisfied with that automatic setting.

Note, the DefaultZone setting is used when no zone is specified,
RoonCommandLine commands all accept a `-z zone` argument that can be
used to specify the zone to be used as well as a `-G <group>` that can
be used to specify the zone grouping to use.

Note also that should you change the name of a Roon audio device in the future
then that name change will also need to be reflected in the `roon_api.ini` groupings.

## Apple Siri Roon Control Setup

After verifying that Apple Siri is working, SSH Shortcuts are enabled and working,
and RoonCommandLine has been installed and configured on a system in the same
local area network as your Roon Core, it's now time to configure Roon Control
using Apple Siri.

See the wiki article
[Roon Voice Commands with Siri](https://github.com/doctorfree/RoonCommandLine/-/wikis/Roon-Voice-Commands-with-Siri)
for a detailed walkthru of Roon voice control using Siri and Apple Shortcuts.

## References

### SSH Setup for Apple Shortcuts

- [Remote control your Mac with your iPhone and SSH Key Shortcuts](https://dougbeal.com/2019/11/02/remote-control-your-mac-with-your-iphone-and-ssh-key-shortcuts/)
- [Setting up SSH for Shortcuts](https://www.thoughtasylum.com/2020/06/01/setting-up-ssh-for-shortcuts/)

### MagicMirror Google Assistant Setup

- [MagicMirror](https://magicmirror.builders/)
- [MMM-GoogleAssistant wiki](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
- [MMM-Detector wiki](http://wiki.bugsounet.fr/en/MMM-Detector)
