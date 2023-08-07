---
# the default layout is 'page'
icon: fas fa-arrow-circle-down
order: 1
---

## RoonCommandLine Installation

RoonCommandLine v2.0.0 and later can be installed on Linux systems using
either the Debian packaging format or the Red Hat Package Manager (RPM).
Support is also included for installing on Mac OS X and Linux variants
that do not support Debian or Red Hat packages. Other systems will
require a manual installation described below. The scripted Linux installation
procedure may also work under Microsoft's Windows Subsystem for Linux but
it is as yet untested.

- [Debian Package installation](#debian-package-installation)
- [RPM Package installation](#rpm-package-installation)
- [Scripted Linux installation](#scripted-linux-installation)
- [Mac OS X installation](#mac-os-x-installation)
- [Post installation configuration](#post-installation-configuration)
  - [Zone groupings and defaults](#zone-groupings-and-defaults)
  - [SSH public key authentication](#ssh-public-key-authentication)
- [Manual installation](#manual-installation)
- [Upgrades](#upgrades)
- [Remote deployment](#remote-deployment)
- [RoonCommandLine Light deployment](#rooncommandline-light-deployment)
- [Removal](#removal)

### Debian Package installation

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

### RPM Package installation

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

### Scripted Linux installation

**NOTE:** If your Linux system supports Debian or Red Hat package format
installation, it is recommended to use the latest release of the RoonCommandLine
package for your platform. The scripted installation described here is
intended for use on those Linux platforms that do not support Debian or
Red Hat format installation packages.

RoonCommandLine requires Python 3. See the
[Guide to installing Python on Linux](https://docs.python-guide.org/starting/install3/linux/)
for step by step instructions to install Python 3 on Linux.

Once the Python 3 dependency is met, install RoonCommandLine by
cloning the RoonCommandLine repository and executing the `Install` script:

```bash
    git clone `https://github.com/doctorfree/RoonCommandLine.git`
    cd RoonCommandLine
    ./Install
```

**Note:** A cleaner installation can be accomplished by executing the `Install`
script as a user with `sudo` privileges, not the `root` user. If you are not
going to enable SSH support, at least make sure the user has sudo privileges.

### Mac OS X installation

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

### Post installation configuration

Default settings are applied during the installation process. The primary area
of post-installation configuration is setting the ZONEGROUPS and DEFAULT values
in the file `/usr/local/Roon/etc/roon_api.ini`. The RoonCommandLine installation
attempts to automate this configuration and should have provided a good starting
point with default settings in `roon_api.ini` but you may wish to adjust these.

#### Zone groupings and defaults

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

#### SSH public key authentication

If you wish to enable remote exection of the RoonCommandLine tools then
it is necessary to setup SSH public key authentication. See the
[Troubleshooting section](https://rooncommand.dev#troubleshooting) below for tips on configuring
SSH public key authentication. The RoonCommandLine utilities can be
executed locally on the same system they are installed on by enabling
local access with the `roon -L` command. This avoids the need to enable
SSH public key authentication but restricts your use of the RoonCommandLine
tools to the system on which they are installed.

**Note:** The roon shell script is not passing credentials in the
SSH invocations. SSH authentication via public key needs to be enabled and
appropriate keys generated and propogated. This topic is addressed in various
guides on setting up SSH. Alternatively, the roon shell script can be
installed on the same system as the Python Roon API and backend scripts.
In this configuration, SSH is no longer required and the roon commands can
be executed locally. In order to enable local execution rather than remote
execution via SSH, run the command `roon -L`

**Another Note:** References in this document to SSH are not referring to
access to the Roon Core. Rather, the SSH facility can be used to remotely
access the system on which the RoonCommandLine tools are installed. All
communication and access to the Roon Core is accomplished via the Roon API.
No changes are ever made to the Roon Core nor is any access to the Roon
Core allowed other than via the API.

### Manual installation

There are three components to install. First, install the Python Roon API
on a system which is on the same local network as your Roon Core.

Note, verify you have Python 3 and pip already installed. For example,
on an Ubuntu 20.04 system I have installed, it was necessary to first configure
Python 3 as the default Python executable, install pip3, and then
configure pip3 as the default pip:

```bash
    sudo update-alternatives --install /usr/bin/python python /usr/bin/python3 10
    sudo apt install python3-pip
    sudo update-alternatives --install /usr/bin/pip pip /usr/bin/pip3 1
```

Once you have verified Python 3 and pip are installed appropriately, install
the Python Roon API:

```bash
    sudo python3 -m pip install roonapi
```

The second component is the Python Roon API frontend shell scripts
and the Python Roon API backend Python scripts. These both get installed on
the system on which the Python Roon API is installed. Copy this entire repository
to the target system. Change directory into the Roon subdirectory and execute
the "Install" script. This will copy the frontend shell scripts into
/usr/local/Roon/bin and the backend Python scripts into
/usr/local/Roon/api.

For example, on the system where the Python Roon API is installed:

```bash
    $ mkdir -p $HOME/src
    $ cd $HOME/src
    $ git clone git@github.com:doctorfree/RoonCommandLine.git

    # Alternatively, download the latest release:
    # https://github.com/doctorfree/RoonCommandLine/-/releases

    $ cd RoonCommandLine
    $ ./Install

    # Edit the Python Roon API command line configuration file.
    # Several default settings are provided. You may wish to modify these.
    $ vi /usr/local/Roon/etc/roon_api.ini

    # The RoonCoreIP setting should have been configured during install.
    # Verify the RoonCoreIP setting is correct.
    # If you do not know your Roon Core IP, run the discovery script
    $ /usr/local/Roon/bin/get_core_ip
    # Authorize the extension when prompted
    # In a Roon Remote client window click "Settings" -> "Extensions" -> "Enable"
```

The third component is the "roon" shell script and its configuration files.
These should be copied to a location in your shell execution PATH on all of
the systems from which you wish to issue command line Roon controls but chose
not to install the RoonCommandLine package there.

```
    # The username and ip address of the Python Roon API server were
    # configured during installation. Verify these settings in the
    # roon script are correct.
    #
    # Copy the "roon" script to all systems on which you wish to use
    # the Python Roon API command line tools, every system you want to
    # enable as a command line Roon remote. Each system must be able to
    # access the Python Roon API installed system via SSH
    #
    # If you wish to run the roon front end script on the same system on
    # which the Python Roon API is installed, then execute the command
    # "roon -L" on that system. This will enable local execution of the
    # Roon Command Line scripts rather than remote execution via SSH.
```

### Upgrades

If you are upgrading from a previous version of RoonCommandLine, starting
with Version 2.0.5, customizations made to `/usr/local/Roon/etc/roon_api.ini`
will be preserved. Unfortunately, upgrading from versions prior to 2.0.5
will not preserve those customizations without some manual effort.

If you are upgrading from 2.0.4 or earlier it will be necessary to either:

- Backup `roon_api.ini` and reapply your customizations to the newly installed `roon_api.ini`

or

- Prior to applying the upgrade, copy `roon_api.ini` to `/tmp/_roon_api_ini_.save`

The latter, copying `roon_api.ini` to `/tmp/_roon_api_ini_.save`, allows the
upgrade to automatically preserve your customizations.

If you are upgrading from 2.0.5 or later this should not be necessary
but a backup prior to upgrading is recommended anyway.

### Remote deployment

Recommended deployment of the RoonCommandLine package is to install the
entire package on every system from which you wish to execute Roon control
commands. This deployment ensures you have all commands available without
the need to configure SSH public key authentication. If you install the
entire package on every system you wish to use for Roon command line control
then you can disregard the following instructions on "RoonCommandLine Light"
deployment.

### RoonCommandLine Light deployment

Not all systems satisfy the RoonCommandLine requirement of Python 3 and Pip.
On those systems that do not satisfy the Python/Pip requirement it is possible
to install just the `roon` command and RoonCommandLine configuration files.

After copying /usr/local/bin/roon and the /usr/local/Roon/etc/ directory
to the target system on which you wish to run Roon commands, perform the
following setup:

```bash
sudo mkdir -p /usr/local/bin
sudo cp roon /usr/local/bin/roon
sudo chmod 755 /usr/local/bin/roon
# Edit the `server` and `user` settings near the top of the script
sudo vi /usr/local/bin/roon
sudo mkdir /usr/local/Roon
sudo mkdir /usr/local/Roon/etc
sudo cp etc/pyroonconf /usr/local/Roon/etc/pyroonconf
sudo cp etc/roon_api.ini /usr/local/Roon/etc/roon_api.ini
# Make the RoonCommandLine configuration directory writeable by your user
USER=`id -u -n`
GROUP=`id -g -n`
sudo chown -R ${USER}:${GROUP} /usr/local/Roon/etc
sudo chmod 755 /usr/local/Roon/etc
sudo chmod 644 /usr/local/Roon/etc/*
```

**Note** A "RoonCommandLine Light" deployment of this nature not only requires
significant manual setup but will also require the configuration of SSH public
key authentication between the target system and a system on which the
RoonCommandLine package was installed. For this reason, it is recommended that
deployments install the entire package on every system, eliminating the need
for extensive manual configuration and SSH public key authentication.

### Removal

On Debian based Linux systems where the RoonCommandLine package was installed
using the RoonCommandLine Debian format package, remove the RoonCommandLine
package by executing the command:

```bash
    sudo apt remove rooncommandline
```
or
```bash
    sudo dpkg -r rooncommandline
```

On RPM based Linux systems where the RoonCommandLine package was installed
using the RoonCommandLine RPM format package, remove the RoonCommandLine
package by executing the command:

```bash
    sudo yum remove RoonCommandLine
```
or
```bash
    sudo rpm -e RoonCommandLine
```

On Mac OS X systems, the RoonCommandLine scripts, patches,
and configuration can be removed by executing the "Uninstall" script in the
RoonCommandLine source directory:

```bash
    git clone git@github.com:doctorfree/RoonCommandLine.git
    cd RoonCommandLine
    ./Uninstall
```
