---
title: Determine the chipset and driver of a wireless card - compatibility_drivers Aircrack-ng
source: https://www.aircrack-ng.org/doku.php?id=compatibility_drivers
author:
published: 2018-07-21
created: 2026-05-26
description:
tags:
  - tools
  - "#aircrack-ng"
---
## Determine the chipset and driver of a wireless card

## Introduction

**IMPORTANT:**

- Please read and understand the following prior to using this page: [Tutorial: Is My Wireless Card Compatible?](https://www.aircrack-ng.org/doku.php?id=compatible_cards "compatible_cards")
- Microsoft Windows is only supported by Airpcap for now. See [this section](https://www.aircrack-ng.org/doku.php?id=install_drivers#windows "install_drivers") for more details.
- See this [FAQ entry](https://www.aircrack-ng.org/doku.php?id=faq#what_is_the_best_wireless_card_to_buy "faq") if your question is “What is the best wireless card to buy?”.

This section deals with two related areas:

- Determine the chipset of a wireless card
- Determine the driver for a wireless card

The previous version of this page can found [here](https://www.aircrack-ng.org/doku.php?id=compatibility_drivers_old "compatibility_drivers_old").

## Determine the chipset

There are two manufacturers involved with wireless cards. The first is the brand of the card itself. Examples of card manufacturers are Netgear, Ubiquiti, Linksys, Intel and D-Link. There are many, many manufacturers beyond the examples give here.

The second manufacturer is who makes the wireless chipset within the card. For example, Ralink, Atheros, Qualcomm. This is the most important company to know. Unfortunately, it is sometimes the hardest to determine. This is because card manufacturers generally don't want to reveal what they use inside their card. However, for our purposes, it is critical to know the wireless chipset manufacturer. Knowing the wireless chipset manufacturer allows you to determine which operating systems are supported, software drivers you need and what limitations are associated with them. The next section describes the operating systems supported and limitations by chipset.

You first need to determine what wireless chipset your card uses. This can be done by one or more of these techniques:

- Search the internet for “<your card model> chipset” or “<your card model> linux” or “<your card model> wikidevi”. Quite often you can find references to what chipset your card uses and/or other people's experiences.
- Search the [Forum](https://forum.aircrack-ng.org/ "https://forum.aircrack-ng.org/")
- You may also have a look at windows driver file names, it's often the name of the chipset or the driver to use.
- Check the card manufacturers page. Sometimes they say what chipset they use.
- Have a look at **lsusb -vv** output for descriptions, USB id and kernel modules used. If the card is internal, do the same with **lspci -vv**.
- Locate the FCC ID of your device. Enter the information into [FCC Website](https://www.fcc.gov/oet/ea/fccid "https://www.fcc.gov/oet/ea/fccid") and then browse the internal photos of the device. Alternatively, use [https://fcc.io](https://fcc.io/ "https://fcc.io") which is a shortcut.

[![pictures.aircrack-ng.org_fcc_id3.jpg](https://www.aircrack-ng.org/pictures.aircrack-ng.org_fcc_id3.jpg "pictures.aircrack-ng.org_fcc_id3.jpg")](https://www.aircrack-ng.org/lib/exe/fetch.php?tok=eca973&media=http%3A%2F%2Fpictures.aircrack-ng.org%2Ffcc_id3.jpg "http://pictures.aircrack-ng.org/fcc_id3.jpg")

Here are some other resources to assist you in determine what chipset you have:

- Linux-wireless has a [list of drivers in Linux](https://wireless.wiki.kernel.org/en/users/drivers "https://wireless.wiki.kernel.org/en/users/drivers")
- [WikiDevi](https://wikidevi.com/ "https://wikidevi.com") in general is a great resource for wireless devices/drivers/etc but if you are looking by device ID, check out [this page](https://wikidevi.com/wiki/List_of_Wi-Fi_Device_IDs_in_Linux "https://wikidevi.com/wiki/List_of_Wi-Fi_Device_IDs_in_Linux").
- [Wireless Adapter Chipset Directory](http://linux-wless.passys.nl/ "http://linux-wless.passys.nl/") nearly the best resource for this kind of information
- [Atheros chipsets based wireless 802.11a/b/g devices](http://atheros.rapla.net/ "http://atheros.rapla.net/") only Atheros-based cards

## Determine the driver

Once you have determined the chipset, chances are you already have identified the driver on Linux. If not, match the chipset against the “other resources” above to figure out the driver.

On Linux, there can be multiple drivers: - Vendor driver: those do not and will not support monitor mode - Peer-modified vendor driver: In some cases, they may support monitor mode but there could be caveats - Staging driver: Standalone driver has been added to the [Linux Staging tree](http://www.kroah.com/log/linux/linux-staging-update.html "http://www.kroah.com/log/linux/linux-staging-update.html"). However, quality of the driver is unknown and needs more work to be included in the kernel - Kernel/mac80211 driver: In this case, chances are, monitor mode is supported. Injection may or may not be supported

If you are deciding on which card to purchase, check the “ [What is the best wireless card to buy?](https://www.aircrack-ng.org/doku.php?id=faq#what_is_the_best_wireless_card_to_buy "faq")” section on this page. There are many considerations that should go into your purchase decision:

- Hardware compatibility with your existing equipment.
- Price and availability of the card.
- Availability of software drivers for your particular operating system and intended use of the software.
- How active is development for the software drivers you need.
- How much peer support and documentation is available for the card and software drivers.

It is not an easy decision to make. By considering these factors, it will help you make a more informed decision on what to purchase.

## Example: Alfa AWUS036AC

Searching for “Alfa AWUS036AC wikidevi” returns me [this page](https://wikidevi.com/wiki/ALFA_Network_AWUS036AC "https://wikidevi.com/wiki/ALFA_Network_AWUS036AC") on WikiDevi.

[![](https://www.aircrack-ng.org/lib/exe/fetch.php?w=200&tok=873b14&media=awus036ac_wikidevi_1.png)](https://www.aircrack-ng.org/lib/exe/detail.php?id=compatibility_drivers&media=awus036ac_wikidevi_1.png "awus036ac_wikidevi_1.png") The box on the right contain all the information needed to identify the chipset manufacturer and model. In this case, RTL8812AU.

It also lists the IDs (**0bda:8812**) which is what would be returned on Linux with the *lsusb* command, right next to **ID**.

If it were on Windows, even if the drivers were not installed, looking in the device manager, that ID would be found in *Details* pane of the device itself, in the property “Hardware IDs”. This is also displayed in WikiDevi: **USB\\VID\_0BDA&PID\_8812** (this is the same as the IDs on Linux, they're just uppercase and they contain some text around: USB device, VID stands for Vendor ID, PID stands for product ID).

[![](https://www.aircrack-ng.org/lib/exe/fetch.php?w=200&tok=ff36f8&media=awus036ac_wikidevi_2.png)](https://www.aircrack-ng.org/lib/exe/detail.php?id=compatibility_drivers&media=awus036ac_wikidevi_2.png "awus036ac_wikidevi_2.png")

Searching for that ID in WikiDevi or any search engine would also help finding the chipset and driver required. Multiple pages would be returned because multiple adapters share the same USB ID.

The exact same principles apply to internal devices, the only difference is they will be found under **lspci**.

Another way to find the chipset/driver, after exhausting the options above, if you don't have the device itself is to download the driver. It is very useful when searching for laptops that are too new to be in any search engine results.

In this case, the Windows driver of the AWUS036AC. It doesn't really matter which version of Windows, the important information are some filenames (and content).

[![](https://www.aircrack-ng.org/lib/exe/fetch.php?w=200&tok=c61fe6&media=awus036ac_inf_file.png)](https://www.aircrack-ng.org/lib/exe/detail.php?id=compatibility_drivers&media=awus036ac_inf_file.png "awus036ac_inf_file.png")

Sometimes the name of the files (*.cat*, *.inf* and *.sys*) can indicate the chipset codename. Most of the time, they don't and the.inf file needs to be opened in a text editor (supporting UTF-16). Scroll down and there will be lists of IDs that are supported by that driver. In this example, the driver supports both PCI and USB Realtek devices, so, it will help narrow down what compatibility you have to look for on Linux.

If the driver is packed in an executable (*.msi* or *.exe*), unpacking will be required. Sometimes multiple times, such as when it is bundled with a WiFi manager. UniExtract (Universal Extractor) is one of the tools to do so.

compatibility\_drivers.txt · Last modified: by mister\_x