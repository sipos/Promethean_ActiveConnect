# Promethean ActiveConnect

## Introduction

These notes are my own regarding a Promethean ActiveConnect device I was given. They are also about the distributions I tried on it, mostly focused on ones potentially suitable for new Linux users. The detail on my experience of distributions is a bit off-topic to the original purpose, and for most are in a separate file now.

## Device

According to the label on the base, it is model `PRM-ACON1-01`. My device's serial number is in [this file](serial_number.txt) (intentionally not shared publicly, but it begins with a G).

It came with some sort of Windows 10 based system on it, and appears to be the Windows 10 version of the ActiveConnect M-series or ClassFlow Connect device with information [here](https://support.prometheanworld.com/s/topic/0TOPQ0000001ptJ4AQ/activconnect-mseries-classflow-connect?language=en_US). One thing noted from the website is that apparently the upper-right (top, next to eSATA port) USB 3.0 port is "optimised for touch devices" (see [here](https://support.prometheanworld.com/s/article/1510?language=en_US)).

Despite the very similar form-factor, it does not appear to be an Intel NUC based device. The firmware is very different, and the port arrangement and internals are different to any I have encountered.

It seems to be intended as some sort of thin-client or presenting machine, and is not very powerful.

## Quick info

* `DEL` to enter setup, or `F8` for boot menu.
* Set date and time to UTC for Linux (not essential but this is the convention, and makes logs less confusing).
* [Enable Intel TurboBoost in the firmware](#enabling-intel-turboboost) for performance gain.
* UEFI mode seems buggy.

## Box contents

The box came with 

* the device
* a transformer/power supply
* separate US/EU and UK IEC 60320 C5 power cables
* WiFi antenna
* four mounting screws
* VESA mounting plate

## Hardware Specs

* CPU: Intel Celeron N2930 1.83-2.16GHz quad core CPU without Hyper-Threading support, 7.5W TDP
* RAM: 4GB DDR3
* Storage: 64GB FORESEE 2.5" SATA SSD (dmesg output reports using UDMA133, but the device itself says 6.0 Gbps TODO: check speed with benchmark and compare to different SSD)
* GPU: Intel HD Graphics for Atom Z3700 (313 MHz base frequency, 854 MHz burst/max dynamic frequency)
* Audio: Intel Atom HD audio
* Ethernet: Realtek RTL8169 gigabit Ethernet
* WiFi Broadcom BCM4352 WiFi adapter (TODO: WiFi 6?)
* TODO: SDHC/SDXC
* TODO: IR
* TODO: Bluetooth

The CPU is not fast, so it is probably best to use a distro/desktop environment friendly to lower spec hardware, like Cinnamon, LXDE, Xfce etc. TODO: benchmark compared to Raspberry Pi 5 and my laptop CPU

Obviously being an x86_64 CPU, it can run a lot of software unavailable on the Raspberry Pi, including Windows 10.

## Ports

On the front, it has the following:

* power button and a power LED, which is red when powered but the system is powered off, and green when powered on
* disk activity LED (white) and fan LED (blue)
* IR port (TODO: which I haven't experimented with yet, but I assume is a standard consumer IR port)
* full-sized SDHC/SDXC slot (TODO: I haven't tested this yet)
* two USB ports, which are yellow and are not USB 3 ports.
* a headphone/speaker 3.5mm audio jack
* a microphone 3.5mm audio jack

On the back, there are the following:

* power barrel jack (19V, 2.1A, centre positive TODO: size)
* full-sized DisplayPort (TODO: verify functioning and version)) and HDMI (TODO: version) output
* four USB 3.0 type A ports (see note in intro about upper right one being optimised for touch screens)
* gigabit Ethernet (TODO: check speed)
* eSATA port (TODO: verify functioning and speed)
* WiFi antenna connector

There are no ports on the sides, top or bottom, all of which are vented. There are four rubber feet/screws to open the case on the base.

## Internals

Opening the base reveals a 4GB DDR3 PC3-12800 SO-DIMM (TODO: full specs), the WiFi/BT card (TODO: spec and connector), a push-button switch marked SW2, and a 2.5" SSD, which despite being labelled SATA6.0Gbps appears to work at 133Mbps (TODO: double check this).

TODO: disassemble more

## MAC addresses

TODO: store WiFi, Ethernet and Bluetooth MAC addresses in separate files

## Firmware

When booting, you can enter a menu to choose a boot device with `F8`, or the firmware settings with `DEL` or `ESC` (though `ESC` also exists).

It was initially in `Legacy Only` rather then `Win8 UEFI` or `Win7 UEFI` boot mode, despite being used with Windows 10, and there seem to be issues running `grub-install` to update the UEFI boot settings, at least in `Win8 UEFI` mode, which you would expect to be the full standard UEFI mode, so it appears that the UEFI firmware is buggy. It may be that it works if you name the boot loader `(ESP)/EFI/boot/bootx64.efi` as some implementations do not support it being called anything else (TODO: test whether this works).

On the first tab, you can set the date and time. The second tab contains device configuration. The third, temperature and voltage info. The fourth power options, like wake on CIR or LAN, and restoring power after AC power loss. The fifth tab is to set a user or admin firmware password. The sixth tab contains boot options, such as the boot NumLock state, timeout, boot mode, PXE ROM, and boot priorities. The sixth tab also contains an OS selection option, letting you choose `Windows 7` or `windows 8.X`, which I left on `Windows 8.X` as this presumably enables full-capability/standard operation of something not supported by Windows 7. The final tab has options to save or not, exit or reset, or override the boot order.

TODO: version identifiers

### Enabling Intel TurboBoost

The main firmware option I ended up changing is on the second (Advanced) tab, under CPU Configuration, setting Power Technology to `Custom` from `Energy Efficient`. This enables extra options, including one called Turbo Mode, which I changed from `Disabled` to `Enabled`. I think this will enable Intel TurboBoost, allowing the CPU clock speed up to 2.16 GHz when TDP and thermal allows it, rather than being fixed at 1.83 GHz, so potentially a significant performance boost.

### Firmware Settings

Press `DEL` or `ESC` to enter at boot-up.

I have them as follows:

Main: Date and time set to UTC

Advanced: CPU Configuration:

* CPU Thermal Configuration: DTS: Enabled (I changed this, enabling this enables the CPU digital thermal sensor so you can get CPU temperature info)
* Limit CPUID Maximum: Disabled
* Execute Disable Bit: Enabled
* Intel Virtualization Technology: Enabled
* Power Technology: Custom (I changed this, see previous section)
* Turbo Mode: Enabled (I changed this, see previous section)
* CPU C6 report: Enabled
* CPU C7 report: Enabled
* Package C State limit: No Limit

Advanced: SATA Configuration: SATA Mode: AHCI Mode

Advanced: USB Configuration:

* Legacy USB Support: Enabled
* XHCI Hand-off: Enabled
* EHCI Hand-off: Enabled
* USB Mass Storage Driver Support: Enabled
* USB transfer time-out: 20 sec
* Device reset time-out: 20 sec
* Device power-up delay: Auto

Advanced: Onboard Device Configuration:

* Audio controller: Enabled
* Serial Port 1: Enabled
* CIR Controller: Enabled
* Back Light Support: Enabled
* USB Charge support: Disabled (It is AC powered, so you could make charging available, but it seems to be available anyway, and it probably consumes more power in standby to have it on. Given it seems to provide power on USB ports anyway, I guess this is support for some sort of fast charging hack with USB type A ports)

Power:

* Enable ACPI Auto Configuration: Disabled
* Enable Hibernation: Enabled
* ACPI Sleep State: S3 (Suspend to RAM)
* Lock Legacy Resources: Disabled
* Restore AC Power Loss: Last State (I changed this from Power Off, because if you have a headless machine, you probably want it to come back up without you having to press the power button)
* Deep Sleep S5 support: Disabled
* CIR Wakeup support: Disabled
* LAN Wakeup support: Disabled
* Wake Up Alarm: Disabled

Security: Didn't set any password

Boot:

* Setup Prompt Timeout: 2
* Bootup NumLock State: Off (I changed this from On as it annoys me)
* Boot Mode: Legacy Only (experimenting with installing Ubuntu and Linux Mint with this set to Win8 UEFI failed)
* OS Selection: Windows 8.X
* Launch PXE Option ROM: Disabled
* Boot Option \#1: P0: FORESEE 64GB SSD

## Software

It came with some sort of OEM install of Windows 10, but I rebooted it and installed Linux before completing setup. Info online suggests it may have some sort of classroom software on it, which may be interesting to explore, but I wiped my device before imaging it.

### Linux

It has a Broadcom WiFi card that does not work with the open-source b43 driver in the kernel, but the `broadcom-sta-dkms`/`wl` proprietary driver does work fine. 

Despite having recommended Ubuntu, I now recommend Linux Mint Cinnamon Edition for beginners to Linux, after talking to a friend who researched this and tried it before trying Linux for the first time (Thanks Tom). It has a familiar Windows 10-like desktop environment hat is a little faster on slow hardware I think than GNOME 3 that Ubuntu uses, and seemed to work smoothly.

I think Steam is best documented on Ubuntu, but I assume it isn't hard to get working on Linux Mint as they are very similar.

Linux Mint using more native packages, rather than FlatPak or Snap packages, means that it is faster than Ubuntu on slow disks.

For all of the following, you should really check the SSH host key when first connecting, unless you completely trust the network you are using, but I am omitting instructions on how to do that. TODO: add this

I am not trying any KDE based distros for this, as KDE is quite resource intensive. It is another common desktop environment though that I recommend people try sometime.

#### Writing USB live/install images on Linux

For almost everything, if you have an image file named, for example, `example.iso`, and the USB key device is `/dev/sdz` (check devices with `sudo fdisk -l /dev/sda` etc, changing the letter until the size of the disk, the device label and the partitions match the USB key you want to write to - **DO NOT make a mistake with the device, as it will destroy the filesystem on the device**) use `sudo dd if=example.iso of=/dev/sdz bs=8M && sudo sync` (the `bs=8M` tells it to use 8Mb blocks, rather than 512b ones, which will be faster for flash, and the sync command will not return until all data has been flushed to disk so it is safe to remove). **Make sure to use the whole device, not a partition, so, e.g. `/dev/sdz` not `/dev/sdz1`.**

#### Linux Mint Cinnamon Edition 22.2

This is the best I have used so far for beginners. As with everything else I have tried, I used Legacy Only boot mode, and the WiFi drivers do not work without some action, but I found that enabling them with the Driver Manager GUI tool in the install environment worked without having to connect Ethernet, and the WiFi credentials were copied over to the installed system automatically, so I could use them after doing the same in the installed system, without needing Ethernet at any point.

Linux Mint is based on Ubuntu, so much of what is written online about Ubuntu applies to Linux Mint. It does not use the GNOME 3 desktop environment, which is unlike Windows and not great on slow hardware. Cinnamon Edition uses the Cinnamon desktop environment, but Xfce (what I use on Gentoo, flexible, good for slow machines, but less simple and familiar to Windows users than Cinnamon probably) and MATE (continuation of GNOME 2, which I used to use) editions are available.

I used the following image for this (sha256sum): `759c9b5a2ad26eb9844b24f7da1696c705ff5fe07924a749f385f435176c2306  linuxmint-22.2-cinnamon-64bit.iso`

After selecting Start Linux Mint from the GRUB menu, ignoring some errors and output from systemd, and waiting a while for the live environment to boot, I installed it as follows (this will erase anything on the machine already):

* Clicked the LM menu button, and under Administration, clicked Driver Manager
* Waited for it to scan for drivers
* Selected the broadcom-sta-dkms option, and clicked Apply Changes
* Closed Driver Manager
* Clicked on the network settings icon (showing no connection, a pair of arrows with a cross) on the bottom right of the screen in the notification area
* Clicked on my WiFi network SSID and entered the key and pressed Enter
* Checked the internet was working by opening Firefox and navigating to <https://bbc.co.uk/>
* Double clicked the Install Linux Mint desktop icon
* Clicked Continue with English selected as the language
* Clicked on the English (UK) keyboard layout category and then clicked Continue with the English (UK) variant selected
* Selected Install multimedia codecs and clicked Continue
* Selected Erase disk and install Linux Mint (without selecting any of the advanced options, though Use LVM and encryption may be a good option if you plan to store any confidential data) (different wording may be present if it doesn't detect another OS) then clicked Install Now
* Clicked Continue on the confirmation box about partitioning
* Clicked Continue with London selected as my location
* Entered my name as `Nick Cripps` (obviously enter your own name, bearing in mind it will be shown on the login screen in full), computer name as `pyros` (this is what I have chosen for this device, choose something else if you are following this, but use lowercase), `sipos` as username (again, choose something different if you are not me, this is what I use for obscure reasons), entered a password and confirmed it, left Require my password to log in checked (you may wish to disable this if you use disk encryption and do not plan to leave the system unattended while powered, or are using it where a password is unnecessary), and left Encrypt my home folder unchecked (use full disk encryption for greater security, unless you share the computer with someone else you want privacy from) and clicked Continue
* Waited a while for installation to complete
* Clicked Restart Now
* Pressed Enter when told to remove the USB media (unless you set it to boot from USB first, instead of just selecting it one-time from the BIOS boot override options or the F8 menu, this is fine)
* Waited a while for the system to boot, typed my password and pressed Enter
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Driver Manager
* Clicked Mount installation media in the Driver Manager window and entered my password
* Selected broadcom-sta-dkms and clicked Apply Changes and entered my password
* Clicked Restart (you can avoid this if you want to, by using `rmmod` to remove conflicting modules, and `modprobe` to load the `wl` module now it is installed, but restarting is easier to describe)
* Entered my password and pressed Enter again to log in
* Checked the WiFi network was connected (credentials were copied from the live environment)
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Update Manager, and clicked OK in the Update Manager, then Apply the Update to update it, and entered my password
* I clicked Install Updates to install all available updates and entered my password again
* Although it isn't required, I rebooted, since there was a kernel update, obviously logging in again after the reboot
* Launched the firewall configuration tool, entered my password, and enabled it
* Clicked on the Removable drives icon in the notification area in the bottom right of the screen, and clicked the eject icon for one of the Linux Mint USB key, before removing it
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd)
* Opened the firewall configuration utility from the LM Menu, Preferences, Firewall Configuration, and entered my password
* Clicked the Rules tab, clicked the plus button, set Policy: Allow, Direction: In, Category: Network, Subcategory: Services, Application: SSH, and clicked Add. This isn't particularly secure, and you should probably limit it to the local network, if you are going to use untrusted networks, and configure sshd to accept only SSH keys, if the security of the system matters.
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling the firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks

#### Ubuntu 24.04.3 LTS (Noble Numbat)

I tried installing this with the boot mode set to Win8 UEFI, and found it to be somewhat unstable, and it failed with an IO error updating the EFI boot configuration with `grub-install`. 

Installing it in Legacy Only boot mode worked fine, either with Ethernet (in which case the installer updates, and the WiFi drivers were installed automatically for first boot of the installed system) or without. I recommend installing with Ethernet connected, to install an up-to-date system, and because I had an issue installing WiFi drivers when I didn't, which is either a wrongly configured repository, or a temporary Ubuntu server issue, which I didn't get when installing with Ethernet.

Either way, the WiFi card does not work during installation, but when installing it with Ethernet connected and selecting Install third-party software for graphics and WiFi, it worked automatically after rebooting in the installed environment. If you didn't enable this, you should be able to enable the Broadcom STA DKMS proprietary driver with the Additional Drivers GUI tool/the Additional Drivers tab in Software and Updates. Alternatively, run `sudo apt install -y broadcom-sta-dkms` in the terminal, and either reboot, or remove the modules it clashes with `rmmod` and then load it with `sudo modprobe wl` (A reboot isn't necessary, but is quicker to describe fully).

I used the following image for this (sha256sum): `faabcf33ae53976d2b8207a001ff32f4e5daae013505ac7188c9ea63988f8328  ubuntu-24.04.3-desktop-amd64.iso`

After selecting Try or Install Ubuntu from the GRUB menu, and waiting a while for the live environment to boot, ignoring the error message about the b43 driver and the Bluetooth firmware failing to load, I installed Ubuntu as follows (this will erase anything on the machine already):

* Clicked Next with English selected for the language
* Clicked Next without making any changes to Accessibility options
* Selected the English (UK) category for keyboard layout, and left the variant as English (UK), and clicked Next
* Clicked Next with Use wired connection selected (I was using Ethernet that is autoconfigured for internet access with DHCP)
* Clicked Update now when an update for the installer was offered
* Clicked Close installer when told to close and relaunch it
* Double-clicked the Install Ubuntu 24.04.3 LTS desktop icon to open the updated installer
* Repeated the above, until the Type of installation screen
* Clicked Next with Interactive installation selected (if I was automating it, this many steps to get to where it was automated would be unacceptable)
* Clicked Next with Default selection selected (you can always install more apps later as needed)
* Ticked both Install third-party software for graphics and Wi-Fi hardware and Download and install support for additional media formats, and clicked Next
* Selected Erase disk and install Ubuntu (without selecting any of the advanced options, though Use LVM and encryption may be a good option if you plan to store any confidential data) (different wording may be present if it doesn't detect another OS) then clicked Next
* Entered my name as `Nick Cripps` (obviously enter your own name, bearing in mind it will be shown on the login screen in full), computer name as `pyros` (this is what I have chosen for this device, choose something else if you are following this, but use lowercase), `sipos` as username (again, choose something different if you are not me, this is what I use for obscure reasons), entered a password and confirmed it, left Require my password to log in checked (you may wish to disable this if you use disk encryption and do not plan to leave the system unattended while powered, or are using it where a password is unnecessary), and left Use Active Directory unchecked (when I have joined Ubuntu machines to AD I have needed to do it after installation anyway, but it may work if you need this and the domain is properly configured), and clicked Next
* I left the time-zone set to Europe/London, and clicked Next (though you will likely need to set it if you don't have an internet connection when installing). The time displayed at the top of the screen should now be local time, and should have been UTC before clicking Next, assuming you set it to that in the firmware.
* Checked the options and clicked Install
* Waited a while for installation to complete
* Clicked Restart now
* Pressed Enter when told to remove the USB media (unless you set it to boot from USB first, instead of just selecting it one-time from the BIOS boot override options or the F8 menu, this is fine)
* Waited a while for the system to boot, clicked my name, typed my password and pressed Enter
* Clicked Next in the welcome window
* Clicked Skip with Skip for now selected for Ubuntu Pro (you can enrol it separately later if you have a subscription)
* Selected No, don't share system data and clicked Next
* Clicked Finish
* I then clicked on the status icons in the top right, the arrow next to WiFi (the WiFi drivers had been automatically installed), selected my WiFi network SSID, entered the key, and pressed Enter
* I could now disconnect the Ethernet and the WiFi worked
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Some sort of firewall may be advisable if you are using untrusted networks. I don't think it enables anything by default.

#### Other distros

See [other_distros.md](other_distros.md).

#### Pop!_OS

I don't necessarily recommend Pop!_OS. It uses GNOME 3, like Ubuntu (though both modified versions), and is less polished and slightly less compatible/well documented than Ubuntu, with no advantages I am aware of. I also found it less stable than Ubuntu or Linux Mint Cinnamon. I would recommend Linux Mint Cinnamon, and then Ubuntu, over Pop!_OS, unless using a System 76 system.

See [other_distros.md](other_distros.md#pop-os).

#### Elementary OS

I don't recommend this. The website was down when I first tried to download it, and it isn't as easy to use, polished, well documented, or performant as other options. It looks quite nice, so may be nice if it works better in future. It uses a desktop environment called Pantheon, heavily based on GNOME 3. It feels like a mix of mac OS, Windows and GNOME 3. It bills itself as the "ethical" (among other things) alternative to Windows and mac OS. It asks you to pay what you can to download it. As I am only trying it, I selected $0. I don't see how it is ethical to be asking for money for what is largely free/libre open-source software. To be fair to it, regarding issues below, the CPU is below what it says is the minimum system requirements (modern Core i3).

See [other_distros.md](other_distros.md#elementary-os).

### Suggested software

For any Linux beginners, I usually install the following GUI apps:

* Firefox (web browser, installed on basically everything already)
* VLC (media player)
* LibreOffice (opens and edits MS Office documents and provides a spreadsheet, presentation and word processing app, among other things)

I use git, and Python extensively, and like using it with virtualenv, and also install a C/C++ compiler and Make etc with `sudo apt install -y build-essential python3 python3-virtualenv git` (for Debian based systems, like Ubuntu and Linux Mint).

I prefer JetBrains PyCharm and CLion as IDEs (though I have the paid professional versions, you want the community one for PyCharm if you don't have a subscription/license for the professional ones). I like vim as a text editor, but it is not at all beginner friendly (use `:q!` to quit without saving, `:qw` to quit saving, and `i` to enter insert mode at the current cursor position and `ESC` to quit insert mode) so probably use nano on the command-line, which basically everything comes with, or gedit, mousepad or kate on GNOME/Cinnamon, Xfce or KDE.

I like to run a SSH daemon so I can log in remotely to most systems. Install it with `sudo apt install -y openssh-server` on Debian/Ubuntu based systems. Note the IP address from the output of `ip addr`, and login with `ssh username@ipaddress` from another system with an SSH client (like Windows 11 or basically any Linux system).

I also often find GIMP and Inkscape useful.

There are numerous free games for Linux, as well as many with Linux support. For emulation, I recommend RetroArch. I build it from source, with a script that is beyond the scope of these notes.

## Plans

I plan to try other beginner friendly distros, or ones I am curious about (other Linux Mint Editions, MX Linux and Nitrux, document trying Debian and Gentoo to compare performance, perhaps a KDE based distro, and perhaps try NixOS (which is not particularly beginner friendly)), and Windows 10 or 11, before eventually installing Gentoo, my preferred distro (which I do not recommend, especially if you are not an experienced Linux user who likes understanding what is happening under the hood and values flexibility over simplicity - people who should use Gentoo are the people who will do so despite recommendations against it, so it doesn't need to be recommended, but I love it).

I plan to install Gentoo, either primarily using packages from the Gentoo binhost, or building them in the cloud on my own virtual binhost, and use the device as a media centre machine. XBMC or similar might be a good fit for this, but I plan to use Gentoo and develop my own media centre environment, because that seems more fun.

I want to try using the consumer IR port with the Flipper Zero, but I plan to use a 2.4GHz or Bluetooth keyboard and trackpad, game controller or WiFi or Bluetooth remote control device as the remote for a media centre. See TODO for other things I plan (at some point, eventually) to check.
