---
title: Using apt Commands in Linux [Ultimate Guide]
source: https://itsfoss.com/apt-command-guide/
author:
  - "[[Abhishek Prakash]]"
published: 2017-07-14
created: 2026-05-26
description: This guide shows you how to use apt commands in Linux with examples so that you can manage packages effectively.
tags:
  - "#commands"
---
[[Using apt-get Commands in Linux Ultimate Guide]]

If you are using Debian, Ubuntu, Linux Mint or any other [Debian or Ubuntu](https://itsfoss.com/debian-vs-ubuntu/) based distributions, you must have come across some apt commands by now.

First noticed in Ubuntu 16.04, apt is slowly gaining popularity. As more and more Ubuntu-based Linux distributions are pushing for apt to be the recommended command for package management, it is time that you learn **how to use apt commands**.

In this guide for Linux beginners, I am going to explain you various apt commands with examples so that you can use them as an expert Linux user.

## What is apt?

Debian Linux uses [dpkg packaging system](https://wiki.debian.org/DebianPackageManagement?ref=itsfoss.com). A packaging system is a way to provide programs and applications for installation. This way, you don’t have to build a program from the source code which, trust me, is not a pretty way to handle packages. [APT](https://wiki.debian.org/Apt?ref=itsfoss.com) (Advanced Package Tool) is the command line tool to interact with the packaging system in Debian-based Linux distributions.

There is already dpkg commands to manage it. But APT is a more friendly way to handle packaging. You can use it to find and install new packages, upgrade packages, remove the packages etc.

The apt commands provide a command line way to interact with APT and manage packages.

At this point, I must mention [apt-get](https://linux.die.net/man/8/apt-get?ref=itsfoss.com) was perhaps the most popular tool around APT. But apt has gained ground lately. In case you are curious, I have already explained the [difference between apt and apt-get](https://itsfoss.com/apt-vs-apt-get-difference/) in a previous article.

## Using apt commands to manage packages

I am using Ubuntu in this tutorial but you can use any other Debian/Ubuntu based Linux distributions such as Linux Mint, elementary OS, Linux Lite etc.

Also, I am using [Pop icon and theme in Ubuntu](https://itsfoss.com/pop-icon-gtk-theme-ubuntu/), so my terminal looks different than the usual purple-themed terminal.

If you prefer, you can watch this video of essential apt commands for Ubuntu users.

![](https://www.youtube.com/watch?v=ECWKViCaI_A)

### Update package database with apt

apt actually works on a database of available packages. If the database is not updated, the system won’t know if there are any newer packages available. This is why updating the repository should be the first thing to do in in any Linux system after a fresh install.

Updating the package database requires superuser privileges so you’ll need to use sudo.

```
sudo apt update
```

When you run this command, you’ll see the package information being retrieved from various servers.

![apt command example with apt update](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples.png)

apt update will update the package database

You’ll see three types of lines here, Hit, Get and Ign. Basically these are:

- Hit: there is no change in the package version from the previous version
- Ign: the package is being ignored. Either the package is way too recent that it doesn’t even bother to check or there was an error in retrieving the file but error was trivial and thus it is being ignored. Don’t worry, this is not an error.
- Get: There is a new version available. It will download the information about the version (not the package itself). You can see that there is download information (size in kb) with the ‘get’ line in the screenshot above.

### Upgrade installed packages with apt

Once you have updated the package database, you can now upgrade the installed packages. The most convenient way is to upgrade all the packages that have available updates. You can simply use the command below:

```
sudo apt upgrade
```

This will show you how many and which all packages are going to be upgraded.

![Using apt commands in Ubuntu](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-1.png)

Upgrade all packages at once

There is another way to provide a complete upgrade by using the command below:

```
sudo apt full-upgrade
```

full-upgrade works the same as upgrade except that if system upgrade needs the removal of a package already installed on the system, it will do that. Whereas, the normal upgrade command won’t do this.

#### What is the difference between apt update and apt upgrade?

Though it sounds like when you do an apt update, it will update the packages and you’ll get the latest version of the package. But that’s not true. apt update only updates the database of the packages.

For example, if you have XYZ package version 1.3 installed, after apt update, the database will be aware that a newer version 1.4 is available. When you do an apt upgrade after apt update, it upgrades (or updates, whichever term you prefer) the installed packages to the newer version.

This is the reason why the fastest and the most convenient way to [update Ubuntu system](https://itsfoss.com/update-ubuntu/) by using this command:

```
sudo apt update && sudo apt upgrade -y
```

### How to install new packages with apt

If you already know the name of the package, you can install it using the command below:

```
sudo apt install <package_name>
```

Just replace the <package\_name> with the desired package. Suppose you want to install mplayer, you can simply use the command below:

```
sudo apt install mplayer
```
![Install package using apt command in Linux](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-3.png)

Install package using apt

The good thing here is that you can use auto-completion. So, if you are not sure about the exact package name, you can type a few letters and press tab and it will suggest all the packages available with those letters. For example:

![Use apt command to install packages in Linux](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-2.png)

Use auto-completion to find packages with given name

### How to install multiple packages with apt

You are not bound to install just one package at a time. You can install several packages at a time by providing the package names all together:

```
sudo apt install <package_1> <package_2> <package_3>
```

#### What if you run apt install on an already installed package?

No need to worry. This will just look into the database and if a newer version is found, it will upgrade the installed package to the newer one. So no harm is done by using it, unless you don’t want it to be upgraded.

#### How to install packages without upgrading

If for some reason you want to install a package, but don’t want to upgrade, it if it is already installed. In that case, you can use the option –no-upgrade in the following manner:

```
sudo apt install <package_name> --no-upgrade
```
![use apt commands in Ubuntu](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-4.png)

Install without upgrading

#### How to only upgrade packages, not install it

If you only want to upgrade a package but don’t want to install it (if it’s not already installed), you can do that with the following command:

```
sudo apt install <package_name> --only-upgrade
```
![Using apt commands with examples](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-5.png)

Only upgrade a package

#### How to install a specific version of an application

By default, the latest version available in the repository will be installed for an application. But if you don’t want to install the latest version, you can specify the version number. You would need to know the exact version number that you want to install.

Just add =version with the name of the package.

```
sudo apt install <package_name>=<version_number>
```

### How to remove installed packages with apt

Enough talk about installing packages, let’s see how to remove packages. Removing packages is as easy as installing them. Just use the command below:

```
sudo apt remove <package_name>
```
![apt command examples](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-6-e1499720021872.png)

Remove a package

Auto-completion works here as well. So you just start typing package name and press tab and it will suggest all the installed packages starting with those letters.

Another way of uninstalling packages is to use purge. The command is used in the following manner:

```
sudo apt purge <package_name>
```

#### What is the difference between apt remove and apt purge?

- `apt remove` just removes the binaries of a package. It leaves residue configuration files.
- `apt purge` removes everything related to a package including the configuration files.

If you used `apt remove` to a get rid of a particular software and then install it again, your software will have the same configuration files. Of course, you will be asked to override the existing configuration files when you install it again.

Purge is useful when you have messed up with the configuration of a program. You want to completely erase its traces from the system and perhaps start afresh. And yes, you can use `apt purge` on an already removed package.

Usually, `apt remove` is more than enough for uninstalling a package.

### Search for packages

Not my preferred way of searching for packages. But this is useful when you are looking for some specific lib. Just use the following command with desired search terms. It will find all the packages containing your search term.

```
apt search <search term>
```
![Search for a package using apt command in Linux](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-8.png)

Search for a package

### See the content of a package

If you want to know more about a package before installing or removing it, you can use the below command:

```
apt show <package_name>
```

This will show information about the given package(s) like its dependencies, installation and download size, different sources the package is available from, the description of the content of the package among other things:

![Show the package information in apt](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-7.png)

Show the package information

### List upgradable and installed versions

apt command has a new option called list. Using this command, you can [see all the packages that have a newer version ready to be upgraded](https://itsfoss.com/apt-list-upgradable/):

```
apt list --upgradable
```
![List all upgradeable packages using apt command in Linux](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-9.png)

List all upgradeable packages

You can also see all the installed packages on the system with installed option:

```
apt list --installed
```

There is also a third option called –all-versions. It will list all the packages available for your system:

```
apt list --all-versions
```

### How to clean your system with apt

I have talked about ways of [cleaning Ubuntu system](https://itsfoss.com/free-up-space-ubuntu-linux/) to free up space. Unlike apt-get, you don’t have clean and autoclean commands here. You can still use the autoremove option and free up some diskspace:

```
sudo apt autoremove
```

This command removes libs and packages that were installed automatically to satisfy the dependencies of an installed package. If the package is removed, these automatically installed packages, though useless, remains in the system.

![Use aot command to free up space in Ubuntu Linux](https://itsfoss.com/content/images/wordpress/2017/07/apt-commands-examples-10.png)

Use autoremove to free up space

I recently cleaned my system and that is why it shows only a few Kb of files to be removed. Otherwise, you could easily get 100s of Mb of free space with this command.

### Learn more about package management

The sources.list is another important part of the apt mechanism that you should know about.

Ubuntu users should also know [how PPA works](https://itsfoss.com/ppa-guide/).

I have deliberately not included apt edit-sources command in this article. It’s because this command option is a work in progress and at this point, it does nothing more than opening the [sources.list file](https://itsfoss.com/sources-list-ubuntu/) in the editor of your choice.

How do you like this guide for using apt commands in Linux? I hope it was easy to understand apt commands with examples. Your feedback will help in creating more such guides in the near future.