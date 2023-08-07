---
title: Roon Voice Commands with Google Assistant
author: doctorfree
date: 2023-08-04 11:25:00 +0800
categories: [Blogging, Tutorial, Information]
tags: [info tutorial voice google assistant]
pin: true
img_path: "/posts/20230804"
---

## Overview

Activating and configuring the
[MMM-GoogleAssistant](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
and [MMM-Detector](http://wiki.bugsounet.fr/en/MMM-Detector)
modules on a [MagicMirror](https://magicmirror.builders/) can enable
the use of recipes to control Roon with voice commands using Google Assistant.

Google Assistant voice control of Roon utilizes a command line interface
that issues commands to the Roon Core. The shell command is executed by a
MagicMirror module without the need for SSH.

To utilize this method of Roon voice control it is necessary to get a voice
assistant working then create voice triggers in that assistant that
activate a corresponding action which executes a RoonCommandLine command.

I will describe in detail this method for voice control of Roon
using Google Assistant and the setup precedure required.

### Google Assistant Requirements

This method for voice control of Roon requires a
[MagicMirror](https://magicmirror.builders/) with the
[MMM-GoogleAssistant wiki](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
and [MMM-Detector wiki](http://wiki.bugsounet.fr/en/MMM-Detector) modules
activated and configured properly. Setup for this method is considerably
more difficult but once accomplished results in a superior quality setup
with far more ease and flexibility of use. The Siri setup requires SSH and
the Apple Shortcuts are more difficult to setup and maintain than the
Google Assistant voice recipes. However, Apple Shortcuts do offer advantages
over Google Assistant, especially in a noisy environment where voice commands
may be unreliable. I use both.

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

### RoonCommandLine Setup

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

#### RoonCommandLine Requirements

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

#### RoonCommandLine Installation

RoonCommandLine v2.0.0 and later can be installed on Linux systems using
either the Debian packaging format or the Red Hat Package Manager (RPM).
Support is also included for installing on Mac OS X. Other systems will
require a manual installation described below. The Mac OS X installation
procedure may also work under Microsoft's Windows Subsystem for Linux but
it is as yet untested.

##### Debian Package installation

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

##### RPM Package installation

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

##### Mac OS X installation

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

##### Post installation configuration

Default settings are applied during the installation process. The primary area
of post-installation configuration is setting the ZONEGROUPS and DEFAULT values
in the file `/usr/local/Roon/etc/roon_api.ini`. The RoonCommandLine installation
attempts to automate this configuration and should have provided a good starting
point with default settings in `roon_api.ini` but you may wish to adjust these.

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

### MirrorCommand Setup

Many Google Assistant voice triggers are preconfigured as MMM-GoogleAssistant
recipes in the [MirrorCommand package](https://github.com/doctorfree/MirrorCommand).
Installation of MirrorCommand is not required but greatly eases initial setup
of the Google Assistant recipes for voice control of Roon. Installation is
recommended. See the
[MirrorCommand README](https://github.com/doctorfree/MirrorCommand/-/blob/master/README)
for installation and setup instructions. The initial installation is similar to
that for the RoonCommandLine package:

### MirrorCommand Installation

Many Google Assistant voice triggers are preconfigured as MMM-GoogleAssistant
To install MirrorCommand on the MagicMirror system:

[Download the latest Debian or RPM format packages](https://github.com/doctorfree/MirrorCommand/-/releases)

**NOTE:** The automated configuration requires access to some X11 graphical utilities. Depending upon your system's X11 configuration, it may be necessary to grant the _root_ user access to the display. To do so, prior to installation issue the command:

`xhost +si:localuser:root`

or grant everyone access with

`xhost +`

Install the package on Debian based systems by executing the command

```bash
sudo apt install ./MirrorCommand_<version>-<release>.deb
```

Install the package on RPM based systems by executing the command

```bash
sudo yum localinstall ./MirrorCommand-<version>-<release>.rpm
```

Post installation, configure `/usr/local/MagicMirror/etc/mirrorkeys` with any keys used by your modules. Once keys are configured, execute the command:

```bash
/usr/local/bin/showkeys
```

**NOTE:** The MirrorCommand installation will install MagicMirror and required
modules if you have not already installed MagicMirror. This automated installation
and configuration of MagicMirror and modules is the preferred installation procedure.

### MagicMirror Configuration

MagicMirror with the MirrorCommand package uses config files in
`/usr/local/MagicMirror/config/` to control the behavior of the MagicMirror.
The MirrorCommand package installs many preconfigured MagicMirror config
files including `/usr/local/MagicMirror/config/config-roon.js`. This MagicMirror
config file can be used as an example of how to enable the Google Assistant
recipes for voice control of Roon. In `config-roon.js` see the `recipes:`
section and note the inclusion of the `RoonCommand.js` recipe. Include this
Google Assistant recipe in your MagicMirror config file to enable the
preconfigured Roon voice commands.

### Activate Roon Voice Control

Once a MagicMirror config file has been created with the `RoonCommand.js`
Google Assistant recipe included in the `recipes:` section of the
MMM-GoogleAssistant module, activate Roon voice control via the command line.
Assuming the MagicMirror config file you wish to activate is
`/usr/local/MagicMirror/config/config-roon.js`, execute the command:

`mirror roon`

This should copy the `config-roon.js` file into `config.js` and start
MagicMirror using this config file. If startup is successful the preconfigured
Roon voice commands should be available. These voice commands include:

- "play default album"
- "play default artist"
- "play default genre"
- "play default playlist"
- "play default tag"
- "play default radio"
- "music stop"
- "music off"
- "music mute"
- "music on"
- "music unmute"
- "play album &lt;album name&gt;"
- "play artist &lt;artist name&gt;"

The MMM-Detector module is used to detect Google Assistant voice activation.
In the MMM-Detector configuration section of the MagicMirror `config.js` a
keyword or key phrase is defined. See the `Model:` setting(s) in the
MMM-Detector config. When this "Model" phrase is spoken it wakes up MMM-Detector
and the module listens for a command or query. For example, the default
`config-roon.js` uses the Model keyword "computer" to instruct MMM-Detector
to listen for a command. Other "Model" settings use "ok google" or "hey google"
to wakeup MMM-Detector.

Test the MagicMirror Google Assistant by saying something like
"computer, what time is it" or "hey google, what is the weather". Pause briefly
between the keyword/keyphrase and the query/command. If this is not working,
a common problem is misconfiguratioin of the MagicMirror audio input and output
devices. ALSA audio input/ouput configuration can be performed by executing the
command `sudo /usr/local/bin/set_asound_conf -e`. After reconfiguring ALSA,
try the simple Google Assistant commands again.

Test voice control of Roon with a simple command like "computer, play default radio".
Stop playback by saying "computer, music stop". If this is working try something
a little more difficult like "computer, play artist Deep Purple".

### References

- [MagicMirror](https://magicmirror.builders/)
- [MMM-GoogleAssistant wiki](http://wiki.bugsounet.fr/en/MMM-GoogleAssistant)
- [MMM-Detector wiki](http://wiki.bugsounet.fr/en/MMM-Detector)
