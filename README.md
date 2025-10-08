# Promethean ActiveConnect

## Introduction

These notes are my own regarding a Promethean ActiveConnect device I was given. They are also about the distributions I tried on it, mostly focused on ones potentially suitable for new Linux users. The detail on my experience of distributions is a bit off-topic to the original purpose.

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

#### Pop!_OS

I don't necessarily recommend Pop!_OS. It uses GNOME 3, like Ubuntu (though both modified versions), and is less polished and slightly less compatible/well documented than Ubuntu, with no advantages I am aware of. I also found it less stable than Ubuntu or Linux Mint Cinnamon. I would recommend Linux Mint Cinnamon, and then Ubuntu, over Pop!_OS, unless using a System 76 system.

I used the following image for this (sha256sum): `4e1c5e391062c79dc611ce383c2a709fecac36798ebd81444a734fd41252608e  pop-os_22.04_amd64_intel_58.iso`

I booted Pop!_OS 22.04 LTS, which took a while, and then installed it as follows (with Ethernet connected - I didn't test without it):

* Clicked Wait on the dialogue saying Install Pop!_OS is not responding
* Clicked Select with English selected
* Selected United Kingdom, and clicked Select
* Clicked Select with English (UK) selected for the keyboard layout
* Clicked Select with Default selected for the keyboard layout variant
* Selected Clean Install, and clicked Clean Install
* Selected the ATA FORESEE 64GB SSD, and clicked Erase and Install
* Entered `Nick Cripps` as my full name, and `sipos` as my user name (as before, obviously change these), and clicked Next
* Entered and confirmed a password, and clicked Next
* Left Encryption password is the same as user account password checked and clicked Encrypt (I don't necessarily recommend encrypting the disk if you aren't storing anything sensitive or taking the device anywhere)
* Waited for the system to be installed
* Clicked Restart Device
* Entered the disk encryption/user password, and pressed Enter (which produces the message `cryptsetup: cryptdata: set up successfully`)
* Clicked my name, entered my password, and pressed Enter
* Clicked Next with Dock extends to the edges selected
* Clicked Next with the default workspaces and applications buttons enabled (though I'd disable the workspaces button if you don't use multiple workspaces) and the date & time and notifications position being centre
* Clicked Next on the super key (Windows key on keyboards with that) screen
* Clicked Next on the gestures screen (without hardware to perform them, like a multi-touch touchscreen or track pad, this is irrelevant)
* Clicked Next with the dark theme selected
* Clicked Next without enabling location services
* Typed London into the search box, selected the "London, East and South East England, United Kingdom" option, clicked Next
* Clicked Skip on connecting online accounts
* Clicked Start Using Pop!_OS
* Clicked the Pop!_Shop on the menu bar, clicked the hamburger menu, clicked on Updates & Installed Software, clicked Update All, and waited for Installing updates and Checking for updates to finish, before closing the Pop!_Shop
* Opened Settings, clicked on Sharing, and changed the computer name to `pyros` (choose your own if following this)
* Clicked on Power in the Settings window and changed the Power Mode to Performance (the device only uses AC power, so best to have best performance)
* Clicked on Removable Media in the Settings window, and changed the action for Software from Run Software to Ask what to do (you need to hold down the mouse button to keep the menu open)
* Closed the Settings window and opened a Terminal window, and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server broadcom-sta-dkms`
* Clicked on one of the removable disk partitions, to open a file manager window, and clicked the eject button next to it, before removing the install USB and closing the file manager window
* Closed the terminal window when the command had run, and the prompt was shown again
* Rebooted, by clicking on the menu in the top right, clicking Power Off / Log Out, and then Restart... and Restart (restart isn't necessary, but it is easier to describe than how to load the WiFi drivers without rebooting)
* Removed the Ethernet cable during reboot
* Unlocked the disk, and logged in again, as before
* I then clicked on the status icons in the top right, then on Wi-Fi Not Connected (the WiFi drivers are loaded after a reboot), clicked Select Network, selected my WiFi network SSID and clicked Connect, entered the key, and pressed Enter
* The WiFi now worked
* If you install VLC from the Pop!_Shop, check the package size, as there was one about 45Mb and one over a GB. One will be a deb package and the other a Snap or FlatPak I expect. You may also wish to make it the default player for Music and Video in the Settings app > Default Applications
* Similarly, if installing GIMP or Inkscape, change from the FlatPak to the deb package from the Ubuntu repo for a much smaller install
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, and making it the default browser, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Some sort of firewall may be advisable if you are using untrusted networks. I don't think it enables anything by default.

#### Elementary OS

I don't recommend this. The website was down when I first tried to download it, and it isn't as easy to use, polished, well documented, or performant as other options. It looks quite nice, so may be nice if it works better in future. It uses a desktop environment called Pantheon, heavily based on GNOME 3. It feels like a mix of mac OS, Windows and GNOME 3. It bills itself as the "ethical" (among other things) alternative to Windows and mac OS. It asks you to pay what you can to download it. As I am only trying it, I selected $0. I don't see how it is ethical to be asking for money for what is largely free/libre open-source software. To be fair to it, regarding issues below, the CPU is below what it says is the minimum system requirements (modern Core i3).

I booted the USB key for this, using the following (SHA256sum): `c0ee5f9c1fa27a42fe864a6360ca17b3b40504f258ade3e4cfe7b17d94f8acc6  elementaryos-8.0-stable-amd64.20250902rc.iso`, with Ethernet connected, and then did the following:

* Clicked Select with English selected
* Selected United Kingdom and clicked Select
* Clicked Select with English (UK)... selected (for the keyboard layout category)
* Clicked Select with Default selected (for the keyboard layout variant)
* Selected Erase Disk and Install, and clicked Erase Disk and Install
* Selected ATA FORESEE 64GB SSD and clicked Next
* Entered and confirmed an encryption password, and clicked Set Encryption Password
* Selected Include third-party proprietary drivers when installing and clicked Erase and Install
* Waited for the installation to finish
* Clicked Restart Device
* Waited a while for it to reboot
* Removed the install USB key and pressed Enter when told to remove the installation medium (don't expect to need it, but as before, leaving it in is fine)
* Waited a while for it to boot
* Got bored waiting, and powered off the system by holding the power button and then powering it on again.
* Entered the disk encryption password when prompted and pressed Enter, and waited for boot to finish
* Clicked Select with English... selected (I have removed the install USB, so I know this isn't booting it again, but I would have thought it had if I hadn't)
* Selected English (UK)..., then selected Default and clicked Select to set the keyboard layout
* Entered `Nick Cripps` for my full name (enter yours), `sipos` for my user name (choose your own), entered and confirmed a user password, in this case the same as the disk encryption password, but this may be undesirable from a security point of view, and entered `pyros` for the device name (choose your own), and clicked Finish Setup
* Connected to the WiFi network by clicking on the network icon (a double ended arrow with a dotted middle line) in the top right, selecting my WiFi network SSID, and entering the key
* Unplugged the Ethernet cable
* The account tile said "Account disabled" at the bottom, whether I chose classic or secure session with the cog icon, so I decided to reboot with the switches icon in the top right, clicking the power icon, and clicking Restart
* Again, boot hung with a black screen, but I tried typing the disk encryption password and pressing Enter, even though there was no prompt, and it proceeded
* When it booted, the account was no longer showing as disabled, so I entered my password and pressed Enter to log-in
* I clicked Next on the first page of the welcome screen
* I clicked Next again with the default look selected
* I clicked Next again without enabling Night Light
* I clicked Next again without enabling anything being deleted, but if I planned to keep this system, I may have selected Trashed and Old temporary files. I prefer to manage Downloads and Screenshots myself
* I clicked Next without connecting any online accounts
* I selected Get apps made for elementary OS and reviewed by elementary on AppCentre (which I think opened AppCentre, but it took until I was a couple of steps later, so clicking that box probably did nothing as I closed AppCentre when it opened), and clicked Next
* I checked Operating System, as well as the already checked Free & Purchased Apps for Automatic Updates, and clicked Next
* I clicked Get Started
* I noticed tool-tips for application icons on the dock at the bottom appear behind the icons, rather than in-front of them or above, making them difficult to read, which seems bad
* From the notification area in the top right, I clicked a notification about a driver update being available. This opened the updates window on the Operating System tab, so I clicked Download to download OS updates. After waiting for these to download and install, it prompted me to restart (annoyingly reminding me of Windows), so I did that with the switches icon in the top right, power button, and clicking Restart with Install pending updates ticked
* Again, there was no disk encryption password prompt, so I just entered it and pressed Enter
* The text for the updates being installed was messed up, and there was a kernel stack trace in the background, and I doubt this needed to be done with a reboot, at least for most of them, since it just looked like running apt or dpkg
* The update job took ages, but eventually had rebooted (not sure why again - very Windows) and there was a prompt to unlock the disk encryption this time
* After unlocking the disk encryption, and logging in when the login screen was displayed, I clicked the notification icon in the top right, to see a notification telling me to restart the system. It can't possibly be necessary again, so I clicked it, which did nothing. I opened Settings, then System under Administration, which said the OS was up to date now, so I clicked the Hardware tab. This showed some hardware info and the host name, which was editable, but I don't want to change, so I clicked the Firmware tab. This showed only up to date firmware for the BCM20702A0 (the Bluetooth controller I think), so I clicked the Drivers tab, since a notification had previously said there were driver updates available. This just had a tick box against the broadcom-sta-dkms driver, which is obviously in use as the WiFi is working, so I closed this.
* In Settings, under Power, I changed the Power Mode to Performance (no need to save energy on AC)
* Under Security and Privacy, it may be advisable to enable the Firewall, but I didn't this time (I assume it is similar to Linux Mint TBH, using ufw)
* In Language and Region, it said Language support is not installed completely, and kept showing a dialogue saying System Settings isn't responding, so I went back and into Language and Region again, and clicked Complete Installation, entered my password, changed the Region option to United Kingdom from United States, and clicked Set Language and Set System Language
* As it said some language options would not take effect until I logged-out, I did, by clicking the switches icon in the top right, clicking my user icon, and the logout button and Log Out, and logged back in again
* I checked the Region and Language options in Settings, and it was displaying United Kingdom for both, and the Set Language button was greyed out, but the Set System Language button was not, so I clicked that again, and got the message about logging-out again, so I did, and then restarted the system, and then, after typing the disk encryption password to no prompt and a blank screen again, logged-in again
* Even after opening the Language and Region settings, clicking Set system Language again (as again it was not greyed out, but Set Language was), and rebooting (without logging-out first), it remained the same, so either the system language is set properly, or it is not and it can't be done without launching settings as root, which I can't be bothered to do.
* Again no disk encryption password prompt
* Opening the AppCentre, it was checking for updates, so I waited for that, but it didn't notify me of any updates
* I installed LibreOffice from the Office section in AppCentre
* The AppCentre seemed to crash when finishing this, but it seems to be installed
* LibreOffice remained on the dock with a dot under it even after it was closed, and it warned about it running in the background without appropriate permission
* I decided not to install VLC, and instead to try the Music and Videos apps it comes with, and to try the Web (which is epiphany, and largely as I remember it, but video playing on YouTube is unreliable and slow, and testing a mic with a web app I have successfully used before seems to show input in the spectrograph, but not record anything to playback, also the sound settings do not show any apps playing sound when the browser is clearly playing sound continuously), Mail and Code (seems like a simple editor with syntax highlighting, and some sort of project capability, with plugins, not more useful to me really than Mousepad) apps it comes with
* Some apps (like RedNotebook, a graphical diary and journal, or Portal, an unofficial MS Teams client, or Learn 6502 Assembly, Program vintage game consoles, in Development, and Mark versus Paul!, Museum of All Things, and OpenNox, Simutrans, Stone Kingdoms, Tuxemon, zelda3, in fun and games, Profectus in internet, Aqueducts, Gaia Sky, Hand Tex, Marble, Plots, in Maths, Science and Engineering, seem worth a look) TODO: check them out, on a different system and distro if possible
* I installed Maps, since I noticed in the settings there was nothing as a default for this. It appears to use OpenStreetMap by the look and feel of the map, and is apparently based on Atlas.
* The next time I opened AppCentre it had graphical glitches and stopped responding, before being automatically closed. I am not sure how this distro manages to make Linux so unstable.
* This time in opening AppCentre, after the Checking for Updates message disappeared, I clicked the sun icon with an up arrow in it, which, based on the tooltip, is for updates and installed apps. It said everything is up to date.
* AppCentre crashed again while looking at the Accessories category, and again next time when I opened that section before it had finished checking for updates.
* It again crashed while I was trying to browse the accessories section, when I had waited for the update check to finish before opening it, so I gave up on that.
* It had a reasonable array of development apps, including CLion, but weirdly PyCharm Professional but not community. I assume the Professional app can be installed and used as community without the extra features, but didn't try.
* I installed GIMP from the graphics section. Again, it crashed on installation, but it seemed installed. Like with LibreOffice, there was a notification about it running in the background without permission that disappeared when I closed it.
* Next, I installed Inkscape, again from the graphics section. I accidentally started installing IPE instead, but cancelled it to install Inkscape. As before, it crashed on installation, seemed to have installed properly, but did not notify me about it running in the background without permission. I did get a message about it not responding though. I think both that and the running in the background without permission could be related to the slow CPU. The message about it not responding all the time when it seemed to be working fine was really annoying though. Clicking Force Quit when it had closed but the message kept coming up logged me out, presumably because my whole session crashed. At least that got rid of LibreOffice from the dock.
* In theory, the Slate text editor that advertises being as dumb as rocks might be interesting to try, but I already like Mousepad on Xfce for a simple text editor. I don't see myself using elementary OS much, so am not going to bother.
* I noticed the dock tooltips seem to be working properly now (above the icons, not behind them)
* I installed Reco to test recording and audio playback, since I couldn't playback anything I recorded in the web browser, and the AppCentre didn't crash before I got the notification it was installed (though so many not responding dialogues and it seemed to have hung afterward, and eventually crashed) this time. I got the same notification about Reco running in the background without permission, and Music when I played the file I recorded.
* Videos struggled to play a 1080p MP4 file, but a 360p video verified to work on my laptop played fine. Sound settings still said no apps were playing sound when playing sound from a video. Presumably apps are using ALSA and it is PulseAudio or PipeWire, or something like that. Seems a bit crap anyway.
* Dragging files to move them in the file manager doesn't seem to work.
* I added a test GMail account to online accounts, via Mail, to test Mail. I used the settings it suggested, and got a message saying IMAP verification failed, and that you must be working online (which I thought I was) to do this. I expect the default settings don't work for GMail. It [sounds like](https://support.google.com/mail/answer/7126229?visit_id=638955252290258081-4262774673&hl=en&rd=1) GMail doesn't support password based authentication anymore, and Mail in elementary OS doesn't support anything else.
* I also couldn't get Mail to work with a mail.com account I created for the purpose, with the same issue. The machine was definitely online - I could visit <https://mail.com/> fine in Web. The firewall wasn't enabled. There were no app specific settings or permissions for Mail, and no option to open any settngs in the Mail app. Clearly it just doesn't work.

I didn't try the secure session, explore the dyslexia friendly text option, or other accessibility options (of which there are a lot), or look into how application permissions work (TODO: how does it restrict them in practice?)

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
