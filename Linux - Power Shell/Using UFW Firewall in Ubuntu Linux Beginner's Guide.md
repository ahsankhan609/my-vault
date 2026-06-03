---
title: Using UFW Firewall in Ubuntu Linux [Beginner's Guide]
source: https://itsfoss.com/ufw-ubuntu/
author:
  - "[[Abhishek Prakash]]"
published: 2022-11-14
created: 2026-05-26
description: Learn the basics of using UFW firewall to secure your Linux system in this beginner's guide.
tags:
  - commands
  - firewall
---
[[Set Up Firewall with GUFW on Linux Desktop Beginner Guide]]

UFW (Uncomplicated Firewall) is a simple-to-use firewall utility with plenty of options for all kinds of users.

It is actually an interface for *iptables*, which is the classic low-level tool (and harder to get comfortable with) to set up rules for your network.

## Why should you use a Firewall?

A firewall is a way to regulate the incoming and outgoing traffic on your network. This is crucial for servers, but it also makes a regular user’s system much safer, giving you control. If you are one of those people who like to keep things under control on an advanced level even on the desktop, you may consider setting up a firewall.

In short, the firewall is a must for servers. On desktops, it is up to you if you want to set it up.

## Setting up a firewall with UFW

It is important to properly set up firewalls. An incorrect setup may leave the server inaccessible if you are doing it for a remote Linux system, like a cloud or VPS server. For example, you block all incoming traffic on the server you are accessing via SSH. Now you won’t be able to access the server via SSH.

In this tutorial, I’ll go over configuring a firewall that suits your needs, giving you an overview of what can be done using this simple utility. This should be suitable for both [Ubuntu server and desktop users](https://itsfoss.com/ubuntu-server-vs-desktop/).

Please note that I’ll be using the command line method here. There is a GUI frontend called [Gufw](http://gufw.org/?ref=itsfoss.com) for desktop users but I won’t be covering it in this tutorial.

There is a dedicated guide to Gufw if you want to use that.

### Install UFW

If you are using Ubuntu, [UFW](https://help.ubuntu.com/community/UFW?ref=itsfoss.com) should already be installed. If not, you can install it using the following command:

```
sudo apt install ufw
```

For other distributions, please use your package manager for installing UFW.

To check that UFW is properly installed, enter:

```
ufw --version
```

If it is installed, you should see the version details:

```
abhishek@itsfoss:~$ ufw --version
ufw 0.36.1
Copyright 2008-2021 Canonical Ltd.
```

Great! So you have UFW on your system. Let’s see about using it now.

📋

You need to use sudo or be root to run (almost) all the ufw commands.

### Check ufw status and rules

UFW works by setting up rules for incoming and outgoing traffic. These rules consist of **allowing** and **denying** specific sources and destinations.

You can check the firewall rules by using the following command:

```
sudo ufw status
```

This should give you the following output at this stage:

```
Status: inactive
```

The above command would have shown you the firewall rules if the firewall was enabled. By default, UFW is not enabled and doesn’t affect your network. We’ll take care of that in the next section.

![check ufw status](https://itsfoss.com/content/images/wordpress/2022/11/check-ufw-status.png)

Checking UFW status

But here’s the thing, you can see and modify the firewall rules even ufw is not enabled.

```
sudo ufw show added
```

And in my case, it showed this result:

```
abhishek@itsfoss:~$ sudo ufw show added
Added user rules (see 'ufw status' for running firewall):
ufw allow 22/tcp
abhishek@itsfoss:~$
```

Now, I don’t remember if I added this rule manually or not. It’s not a fresh system.

### Default policies

By default, UFW denies all incoming and allows all outgoing traffic. This behavior makes perfect sense for the average desktop user, since you want to be able to connect to various services (such as http/https to access web pages) and don’t want to have anyone connect to your machine.

However, **if you are using a remote server, you must allow traffic on the SSH port** so that you can connect to the system remotely.

You can either allow traffic on SSH default port 22:

```
sudo ufw allow 22
```

In case you are using SSH on some other port, allow it at the service level:

```
sudo ufw allow ssh
```

Do note that the firewall is not active yet. This is a good thing. You can modify rules before you enable ufw so that essential services are not impacted.

If you are going to use UFW in a production server, please ensure to allow ports through UFW for the running services for which the following article will help you.

For example, web servers usually use port 80, so use `sudo ufw allow 80`. You may also do it at service level by `sudo ufw allow apache`.

This onus lies on your side and it is your responsibility to ensure your server runs properly.

For **desktop users**, you can go ahead with the default policies.

```
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

### Enable and disable UFW

For UFW to work, you have to enable it:

```
sudo ufw enable
```

Doing so will start the firewall and schedule it to start every time you boot up. You receive the following message:

```
Firewall is active and enabled on system startup.
```

📋

**Again**: If you are connected to a machine via ssh, make sure ssh is allowed before enabling ufw by entering *sudo ufw allow ssh*.**

If you want to turn UFW off, type in:

```
sudo ufw disable
```

You’ll get back:

```
Firewall stopped and disabled on system startup
```

### Reload firewall for new rules

If UFW is already enabled and you modify the firewall rules, you need to reload it before the changes take into effect.

You can restart UFW by disabling it and enabling it again:

```
sudo ufw disable && sudo ufw enable
```

Or **reload** the rules:

```
sudo ufw reload
```

### Reset to default firewall rules

If at any time you screw up any of your rules and want to return to the default rules (that is, no exceptions for allowing incoming or denying outgoing traffic), you can start it afresh with:

```
sudo ufw reset
```

🚧

Keep in mind that this will delete all your firewall configs.

## Configuring firewall with UFW (more detailed view)

Alright! So you have learned most of the basic ufw commands. At this stage, I would prefer to go a bit in more detail on the firewall rule configuration.

### Allow and deny by protocol and ports

This is how you add new exceptions to your firewall; **allow** enables your machine to receive data from the specified service, while **deny** does the opposite

By default, these commands will add rules for both **IP** and **IPv6**. If you’d like to modify this behavior, you’ll have to edit **/etc/default/ufw**. Change

```
IPV6=yes
```

to

```
IPV6=no
```

That being said, the basic commands are:

```
sudo ufw allow <port>/<optional: protocol>
sudo ufw deny <port>/<optional: protocol>
```

If the rule was successfully added, you’ll get back:

```
Rules updated
Rules updated (v6)
```

For example:

```
sudo ufw allow 80/tcp
sudo ufw deny 22
sudo ufw deny 443/udp
```

📋

***Note*:** If you don’t include a specific protocol, the rule will be applied for both *TCP* and *UDP*.

If you enable(or, if already running, reload) UFW and check out its status, you can see that the new rules have been successfully applied.

![UFW Ports](https://itsfoss.com/content/images/wordpress/2019/03/ufw_ports.png?fit=800%2C443&ssl=1)

List of UFW Ports

You can also allow/deny **port ranges**. For this type of rule, you must specify the protocol. For example:

```
sudo ufw allow 90:100/tcp
```

Will allow all services on ports 90 to 100 using the *TCP* protocol. You can reload and verify the status:

![UFW Port Ranges](https://itsfoss.com/content/images/wordpress/2019/03/ufw_port_ranges-1.png?fit=800%2C430&ssl=1)

UFW Port Ranges

### Allow and deny by services

To make things easier, you can also add rules using the service name:

```
sudo ufw allow <service name>
sudo ufw deny <service name>
```

For example, to allow incoming ssh and block and incoming HTTP services:

```
sudo ufw allow ssh
sudo ufw deny http
```

While doing so, **UFW** will read the services from **/etc/services**. You can check out the list yourself:

```
less /etc/services
```
![List /etc/services](https://itsfoss.com/content/images/wordpress/2019/03/etc_services.png?fit=800%2C615&ssl=1)

List /etc/services

### Add rules for applications

Some apps provide specific named services for ease of use and might even utilize different ports. One such example is **ssh**. You can see a list of such apps that are present on your machine with the following:

```
sudo ufw app list
```
![UFW App List](https://itsfoss.com/content/images/wordpress/2019/03/ufw_app_list.png)

App List of UFW

In my case, the available applications are **CUPS** (a network printing system) and **OpenSSH**.

To add a rule for an application, type:

```
sudo ufw allow <application>
sudo ufw deny <application>
```

For example:

```
sudo ufw allow OpenSSH
```

Reloading and checking the status, you should see that the rule has been added:

![UFW Apps](https://itsfoss.com/content/images/wordpress/2019/03/ufw_apps.png?fit=800%2C478&ssl=1)

UFW apps

## Conclusion

This was just the tip of the ~~iceberg~~ firewall. There is so much more to firewalls in Linux that a book can be written on it. In fact, ***there is already an excellent book Linux Firewalls by Steve Suehring***.

If you think setting up a firewall with UFW, you should try using [*iptables* or *nftables*](https://linuxhandbook.com/iptables-vs-nftables/?ref=itsfoss.com). Then you’ll realize how UFW uncomplicates the firewall configuration.

I hope you liked this beginner’s guide to UFW. Let me know if you have questions or suggestions.