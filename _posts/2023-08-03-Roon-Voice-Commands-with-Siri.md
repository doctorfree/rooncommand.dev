---
title: Roon Voice Commands with Siri
author: doctorfree
date: 2023-08-03 17:17:00 +0800
tags: [info, voice, siri, apple, commands]
pin: true
img_path: "/posts/20230803"
---

## Overview

Siri voice control of Roon utilizes a command line interface
that issues commands to the Roon Core. The shell command is
executed using an SSH Shortcut.

Apple SSH shortcuts can be used to execute commands on systems
that allow SSH access. On an iOS device create shortcuts which
use the “Run script over SSH” option for Apple Scripting shortcuts.
The shortcuts execute a Bash command which is a shell script that
executes the Python script with appropriate arguments.

I will describe in detail this method for voice control of Roon
using Siri and the setup precedure required.

## RoonCommandLine Setup

Voice control of Roon as described in this document requires the
use of a command line interface to issue the Roon commands. This is
accomplished with the
[RoonCommandLine](https://github.com/doctorfree/RoonCommandLine)
package which contains a shell command that acts as a frontend to
the [Python Roon API](https://github.com/pavoni/pyroon).

See the
[RoonCommandLine website](https://rooncommand.dev)
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
[RoonCommandLine Releases](https://github.com/doctorfree/RoonCommandLine/releases).

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
[RoonCommandLine Releases](https://github.com/doctorfree/RoonCommandLine/releases).

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
to SSH in to the system.

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

### RoonCommandLine Test

Once the initial installation and configuration of RoonCommandLine on a system
in your local network is accomplished, test the system to verify it can
communicate successfully with the Roon Core. Try a simple Roon command like
listing the configured Roon zones:

`roon -l zones`

If zone listing fails then verify your Roon Core is running, reachable, and
`LOCAL=true` in `/usr/local/Roon/etc/pyroonconf`. Verify the Python Roon API
extension is authorized in Roon `Settings -> Extensions`. To authorize the
extension run the command `/usr/local/bin/get_core_ip` and when prompted,
authorize the extension in Roon `Settings -> Extensions`. Note that the
IP address returned for the Roon Core by `get_core_ip` is correct. If a
simple listing of zones with `roon -l zones` still fails then check the
[Troubleshooting](https://rooncommand.dev#troubleshooting)
section of the
[RoonCommandLine README](https://github.com/doctorfree/RoonCommandLine/blob/master/README.md)

After verifying the RoonCommandLine package is successfully communicating
with the Roon Core, proceed to the next section.

## Apple Siri Setup

To get started with Apple SSH shortcuts first enable SSH access on the system
where the [RoonCommandLine](https://github.com/doctorfree/RoonCommandLine)
package was installed. Follow one of the many guides for setting up SSH
with Apple Shortcuts. For example, these two guides should get you started:

- [Remote control your Mac with your iPhone and SSH Key Shortcuts](https://dougbeal.com/2019/11/02/remote-control-your-mac-with-your-iphone-and-ssh-key-shortcuts/)
- [Setting up SSH for Shortcuts](https://www.thoughtasylum.com/2020/06/01/setting-up-ssh-for-shortcuts/)

Verify that Apple Siri is working and responds to queries like "Hey Siri",
"What time is it?". Verify that SSH Shortcuts are working by creating a
shortcut that performs a simple command like `ping` as described in the
guides above. On recent versions of Apple's iOS the Shortcuts setting for
"Allow Running Scripts" is disabled. You may need to enable "Allow Running
Scripts" in Shortcuts by visiting `Settings -> Shortcuts` on your iOS device
and enabling "Allow Running Scripts".

Once Siri and SSH Shortcuts are confirmed to be working, proceed to the next section.

## Apple Siri Roon Control Setup

After verifying that Apple Siri is working, SSH Shortcuts are enabled and working,
and RoonCommandLine has been installed and configured on a system in the same
local area network as your Roon Core, it's now time to configure Roon Control
using Apple Siri.

### Navigating the Shortcuts App

Open the `Shortcuts` app on your iOS device. Tap `My Shortcuts` and
`All Shortcuts`. Tap the `+` symbol at the top right corner of the
app window to create a new shortcut. Tap `Add Action` then `Scripting`.
Scroll down the list of scripting actions to the `Shell` category. Tap
`Run Script Over SSH`.

### Configuring the Shortcut

This should add the "Run script over SSH" action to the new shortcut.
Tap `Show More` to view and modify the details of the scripting action.
Set the `Host` entry to the IP address of the system on which RoonCommandLine
was installed. For example, 10.0.1.55. Set the `User` entry to the user on
the RoonCommandLine system that you want to run the command as. For example,
my user's username is "ronnie".

Tap `SSH Key` for `Authentication`. In the text box that says `Script`
enter the command you wish to execute. To get started, try something simple
like `roon -r default` which plays the default Roon Live Radio station. Now
that the details of the scripting action have been set, tap `Next` in the
top right of the `New Shortcut` window.

**NOTE:** Some Mac users have reported their SSH Shortcuts do not work unless
they are run in a login shell. This is likely due to some Python environment
settings in the login shell startup. To run a Shortcut in a login shell preface
the command you wish to run with `bash -l -c ...` and surround the command in
quotes. For example, to run the command `roon -r default` in a login shell,
when configuring the Shortcut Script, use the command:

`bash -l -c "roon -r default"`

### Naming the Shortcut

Enter the name of the shortcut. By default, the name of the shortcut will be
used as the phrase Siri will recognize to run this shortcut. Choose a shortcut
name that both reflects the action it performs and will be easily recognized
by Siri. Voice assistants can be picky. For example, using "Roon" in your
shortcut name might seem like a good idea since it is performing a Roon action
but "Roon" will often be heard as "Rune" and Siri will try to execute the
shortcut with "Rune" in its name. For this first shortcut that plays Roon Radio,
let's try the shortcut name "Play Radio".

### Testing the Shortcut

Now we can test voice control of our first shortcut. You should be able to run
this shortcut by saying "Hey Siri, Play Radio". Try it out. After a short delay
your Roon Core should play the default Roon Live Radio station in the default
Roon playback zone. Make sure that zone is active, available, and the necessary
audio device(s) are powered on and ready to play.

#### Adding the Shortcut to the Home Screen

To test the Shortcut without Siri, add the Shortcut to the iOS device Home Screen.
This is an added benefit of using Shortcuts for voice control. In addition
to voice control they can be run from the device allowing remote Roon control even
in a noisy environment where voice control is unavailable. Testing the Shortcut
in this manner allows us to verify the Shortcut works and isolate any problems
encountered.

To add the Shortcut to the iOS device Home Screen, tap the three dots in the
upper right corner of the shortcut then tap the three dots in the upper right
corner of the Shortcut configuration screen. This brings up the "Details"
configuration panel for the Shortcut where you can specify the Shortcut name.
Tap "Add to Home Screen" and "Add". An icon for this Shortcut will now be on
the iOS device Home Screen and the Shortcut can be run by tapping that icon.

Running the Shortcut from the Home Screen icon enables a test of the Shortcut
without using Siri as well as providing the convenience of another quick and
easy way to control Roon remotely.

### Adding More Shortcuts

More complicated commands can be configured. Follow the same procedure as above
but replace `roon -r default` with whatever RoonCommandLine command you like.
For example, to configure a shortcut that plays your "Fav Bowie" playlist in
the "Living Room" zone, add the following command in the `Script` text box:

`roon -p "Fav Bowie" -z "Living Room"`

Rather than creating a new shortcut every time you want to add some new command
to your shortcuts, it is possible to duplicate an existing shortcut and then
modify it. We can use this to avoid having to enter the IP address, Username,
and Authentication type when creating a new shortcut. For example, in the
Shortcuts app, press and hold the `Play Radio` shortcut we created earlier.
In the menu that pops up, tap "Duplicate". A new shortcut should be created
named "Play Radio 1". Tap the three dots (...) in the top right corner of
the shortcut which should bring up the newly created shortcut ready for us to
configure it.

First, rename the shortcut to something describing the action you will add
and will be easily recognized by Siri. To rename the shortcut, tap the
three dots (...) in the top right and replace the current name with a new name.
For example, replace "Play Radio" with "Play Bowie". Note that the name of
the shortcut does not need to be exactly what the action is, in this case
the name of a playlist. It just needs to be descriptive enough to let you
know what it does and it needs to be simple enough to allow Siri to recognize
it distinctly and without confusion. After renaming the shortcut, Tap `Done`.

In the `Run script over SSH` scripting action, tap "Show More". All of the
settings should be correct and need not be modified. The only things we need
to modify are the Script text box command to execute and the name of the shortcut.
Replace the Script text box command `roon -r default` with the command to
play your favorite Roon playlist in your desired Roon zone. For example,
replace `roon -r default` with `roon -p "Fav Bowie" -z "Living Room"`
Tap `Done` in the top right.

Now you can play your Roon playlist by saying "Hey Siri, Play Bowie" or whatever
you named the shortcut to be.

### Troubleshooting Shortcuts

If your Siri command failed to run the shortcut or the shortcut did not
result in the desired action, perform some troubleshooting.

#### Verify Command Line Execution

Start by verifying the command you entered in the Script text box works when
executed at the command line. For example, in a terminal window on the system
where the SSH commands are being executed and as the user you entered in the
Shortcut "User" setting, attempt to run the command at the command line prompt:

`roon -p "Fav Bowie" -z "Living Room"`

Attempt to run the exact same command you entered in the shortcut Script text box.
If it does not succeed as expected then the issue is not in your shortcut or
Siri but in the Roon command line setup. See the
[Troubleshooting section](https://rooncommand.dev#troubleshooting)
of the RoonCommandLine README to resolve this issue.

#### Verify SSH Authentication

If it succeeds then move on to verifying SSH authentication is configured properly.
In the Shortcut app, tap the three dots in the upper right corner of the shortcut
you wish to troubleshoot. Tap "Show More" in the scripting action. Verify that
`Authentication` is set to `SSH Key`. Just below `Authentication` you should see
`SSH Key` on a line with "ed25519 Key" or something similar. Tap "ed25519 Key".
Tap `Share Public Key` and copy it or air drop it or send it to yourself in
Messages. Verify that this public key is in the `~/.ssh/authorized_keys` file
on the system where RoonCommandLine is installed in the home directory of the
user you are using to execute the SSH commands. In my example above this was
the system with IP address 10.0.1.55 and the user `ronnie`. In a terminal window,
logged in as that user on that system, change directory to `~/.ssh` and open
the file `authorized_keys` in a text editor. Verify the copied/air dropped public
key is in that file and, if not, add it to the file.

#### Verify SSH Enabled

The system on which the SSH command is executed (in the example above, 10.0.1.55)
must have SSH access enabled. On Linux this means that the `ssh` service is enabled
and active. On MacOS `System Preferences -> Sharing -> Remote Login` must be
enabled and the user(s) executing the Roon commands must be allowed access.

Verify that the SSH service is enabled and active. On Linux a command similar to:

`systemctl status sshd`

should display the status of the SSH service. On MacOS the command:

`sudo systemsetup -getremotelogin`

will display whether remote login is on or off. On MacOS it may be
necessary to check the "Allow full disk access for remote users" box
in the "Remote Login" dialog.

#### Modify SSH Command

Some systems may require the SSH command to be run in a login shell.
To modify the SSH command to run in a login shell preface the command
you wish to run with `bash -l -c ...` and surround the command in quotes.
For example, to run the command `roon -r default` in a login shell,
when configuring the Shortcut Script, use the command:

`bash -l -c "roon -r default"`

One RoonCommandLine user has reported that SSH Shortcuts fail when invoking
the `roon` command but succeed when invoking the appropriate Python script
directly. For example:

FAILS: `/usr/local/Roon/bin/roon -c playpause -z "HQP4 Dylan"`

SUCCEEDS: `python3 /usr/local/Roon/api/zone_command.py -c playpause -z "HQP4 Dylan"`

No explanation for this behavior has yet been discovered.

## References

- [Remote control your Mac with your iPhone and SSH Key Shortcuts](https://dougbeal.com/2019/11/02/remote-control-your-mac-with-your-iphone-and-ssh-key-shortcuts/)
- [Setting up SSH for Shortcuts](https://www.thoughtasylum.com/2020/06/01/setting-up-ssh-for-shortcuts/)
