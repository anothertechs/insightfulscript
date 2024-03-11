---
title: Beginner Guid to Snap and Snap Store
image: /images/snapcraft.webp
date: 2021-06-22
published: true
description: "Snap is a cross-platform packaging and deployment system developed by  Canonical for the Linux. It is compatible with most major Linux distributions, including Ubuntu,Linux mint, Debian, Arch Linux,Fedora, CentOS, and Manjaro."
Tags: ["linux"]
keywords: snap,snapd,store,snap store,ubuntu,linux,manjaro,arch, arch linux,download,install,package,manager,aur,deb,What is,usage
---

# Beginner guide to Snapcraft,Snap,Snapd and Snap Store

Package Manager is a set of integrated
services that make it easy to install, update, remove, and configure
packages/programs on computers.

Especially with regard to the linux operating system, you can choose
from a wide range of package managers, such as Pacman(Arch/Manjaro), apt(Ubuntu/Debian), yum(Red Hat/Cent Os),dnf(Fedora). Each of these package managers has different
features that can distinguish them from the others.

However, a relatively new package manager, Snap, has become a
viable replacement for traditional package managers. Let's take a look at Snap, its
advantages and disadvantages, and how to install and use it on Linux.

## What is a Snap?

Snap is a cross-platform packaging and deployment system developed by Ubuntu
manufacturer [Canonical](https://canonical.com/) for the Linux platform. It is compatible with most major Linux
distributions, including Ubuntu, Debian, Arch Linux,
Fedora, CentOS, and Manjaro.

### What is Snaps?

Like any other package manager, Snap also includes a package called
snaps. Unlike the traditional package manager counterparts, these packages have no dependencies and are easy to install.

The snaps end with the extension **.snap**, essentially a compressed
file system using the [SquashFS](https://www.kernel.org/doc/html/latest/filesystems/squashfs.html) format, contains the entire
package module, including the app, its dependent libraries, and additional
metadata.

### What is Snapd?

Snapd (or snap daemon) uses snap metadata to configure a
security sandbox for applications on the system. Since it is a daemon process, the entire task of maintaining and managing the instant environment in
happens in the background.

### What is Snap Store?

Snap is located in the Snap Store, and you can browse and download them like other
package managers. In addition, you can also use the
option to publish your own instant packages directly to the [Snap store](https://snapcraft.io/store), which is
something that traditional package managers cannot achieve.

In addition to these elements, Snap has another basic component
, called **channel**. The channel is responsible for defining the version
of the installation snaps and tracking updates on its system. Therefore, when you install or upgrade snaps of
, you can specify which
channel you want to continue to use for each of these operations.

## Installing Snap in Linux

Below is the command to install snap on different linux distros:

On Debian/Ubuntu/Linux Mint based distros:

```bash

sudo apt update && sudo apt install snapd

```

On CentOS/RHEL- based distros:

```bash

yum install epel-release && yum install snapd

```

To install snap on Fedora:

```bash

sudo dnf install snapd

```

On Arch Based Distros:

```bash

sudo pacman -S snapd

```

Once installed, you have to start snap daemon(snapd service).

For **systemd** user you can run the following command:

```bash

sudo systemctl start snapd.socket # To start snapd services
sudo systemctl enable snapd.socket # To start services at boot

```

## Usage of Snap

### Finding in Snap

Command to find app accross different category:

```bash

snap find category_name

#For Example
snap find development

```

### Installing a snap Package

Command to install app accross different category:

```bash

sudo snap install app

#For example
sudo snap install steam

```

After installation, you can find the program in the "Applications" menu of the Linux distribution. Then you can run it directly from the menu or enter its name through the terminal.

### List all the snap apps

Command to list app :

```bash

snap list

```

### To Know the version information of Snap app

Command to know version of snap applications:

```bash
snap list package_name

#For Example
snap list steam
```

### Updating snap apps

Command to update snap applications:

```bash
snap refresh
```

To update a particular package

```bash
snap refresh app

#For Example
snap refresh steam
```

### Removing Snap app

Command to remove snap applications

```bash
snap remove package_name

#For Example
snap remove steam
```

## Advantages of using Snap

1. Each instant package runs independently to avoid interference with other packages on the system. Therefore, when you delete a snap package, the system removes all of its data, including dependencies, without affecting other packages. Needless to say, this also provides a more secure environment, because one package cannot access the information in another package.

2. Snaps comes with dependencies (libraries) and can easily access the program immediately, because you no longer need to manually install missing dependencies to run on your system.
3. The real-time update will automatically adjust according to the set time interval. Therefore, you always run the latest version of the program on your system.

4. Snap makes it easy for developers to distribute their software directly to users, so they don't have to wait for the Linux distribution to start.

5. In addition to the previous point, another benefit of having developers responsible for packaging and distributing their software is that they don't have to create a release-specific package because it comes with the required dependencies.

## Disadvantages of using Snap

1. Because snaps are bundled with dependencies, they are larger and take up more disk space than other package manager counterparts.

2. Due to included dependencies, snaps are distributed as compressed file system images and must be installed prior to installation. Therefore, snaps run slower than traditional software packages.

3. Another downside to allowing developers to distribute software packages is that these software packages have not been rigorously reviewed or vetted by the community, so there is a risk that they contain malware seen a few years ago.

4. Although Snap allows developers to distribute their snaps directly to users, the distribution pipeline requires them to set up a Canonical account and host their snaps there. This goes against the nature of the open-source methodology, because even if the software remains open-source, the package management system is still controlled by the entity.

5. Regarding malware risks, Snap now uses an automated malware test to scan user-uploaded packages for malicious code, and then is distributed on the Snap Store.

6. Since the Snap backend is still closed source and controlled by Canonical, many major Linux distributions disagree with the idea of Snap as the default package manager on their systems.
