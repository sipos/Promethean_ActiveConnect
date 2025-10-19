# Other Linux Distros I Tried on the Promethean ActiveConnect

## Linux Mint Cinnamon Edition 22.2

See [README.md](README.md#linux-mint-cinnamon-edition-222).

## Ubuntu 24.04.3 LTS (Noble Numbat)

See [README.md](README.md#ubuntu-24043-lts-noble-numbat).

## Pop!_OS

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

## Elementary OS

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
* I added a test GMail account to online accounts, via Mail, to test Mail. I used the settings it suggested, and got a message saying IMAP verification failed, and that you must be working online (which I thought I was) to do this. I expect the default settings don't work for GMail. It [sounds like](https://support.google.com/mail/answer/7126229?visit_id=638955252290258081-4262774673&hl=en&rd=1) GMail doesn't support password based authentication any more, and Mail in elementary OS doesn't support anything else.
* I also couldn't get Mail to work with a mail.com account I created for the purpose, with the same issue. The machine was definitely online - I could visit <https://mail.com/> fine in Web. The firewall wasn't enabled. There were no app specific settings or permissions for Mail, and no option to open any settings in the Mail app. Clearly it just doesn't work.

I didn't try the secure session, explore the dyslexia friendly text option, or other accessibility options (of which there are a lot), or look into how application permissions work (TODO: how does it restrict them in practice?)

## Linux Mint Xfce Edition 22.2

Xfce is less easy to use than Cinnamon, but more flexible, and possibly less resource intensive. I suggest Cinnamon to new users on Linux, but use Xfce personally.

The Xfce environment on Linux Mint is rather Windows 10-like, unlike the default Xfce environment, but obviously it can be changed.

I used the following image for this (sha256sum): `dea13e523dca28e3aa48d90167a6368c63e1b3251492115417fdbf648551558f  linuxmint-22.2-xfce-64bit.iso`

* Selected Start Linux Mint from the GRUB menu
* Ignored various errors/messages from the kernel/boot sequence and waited for the desktop to appear
* Clicked the LM menu button, and under System, clicked Driver Manager
* Waited for it to scan for drivers
* Selected the broadcom-sta-dkms option, and clicked Apply Changes
* Closed Driver Manager
* Clicked on the network settings icon (showing no connection, a pair of arrows with a cross) on the bottom right of the screen in the notification area
* Clicked on my WiFi network SSID under Available networks, and entered the key and pressed Enter
* Checked the internet was working by opening Firefox and navigating to <https://bbc.co.uk/>
* Double clicked the Install Linux Mint desktop icon
* Clicked Continue with English selected as the language
* Clicked on the English (UK) keyboard layout category and then clicked Continue with the English (UK) variant selected
* Selected Install multimedia codecs and clicked Continue
* Selected Erase disk and install Linux Mint, clicked Advanced features..., selected Use LVM with the new Linux Mint installation and Encrypt the new Linux Mint installation for security, clicked OK, (different wording may be present if it doesn't detect another OS) then clicked Install Now
* Entered and confirmed a security key and clicked Install Now (I did not enable a recovery key - I won't forget the key, and did not bother to overwrite the empty disk space)
* Clicked Continue on the confirmation box about partitioning
* Clicked Continue with London selected as my location
* Entered my name as `Nick Cripps` (obviously enter your own name, bearing in mind it will be shown on the login screen in full), computer name as `pyros` (this is what I have chosen for this device, choose something else if you are following this, but use lowercase), `sipos` as username (again, choose something different if you are not me, this is what I use for obscure reasons), entered a password and confirmed it, left Require my password to log in checked (you may wish to disable this if you use disk encryption and do not plan to leave the system unattended while powered, or are using it where a password is unnecessary), and left Encrypt my home folder unchecked (use full disk encryption for greater security, unless you share the computer with someone else you want privacy from) and clicked Continue
* Waited a while for installation to complete
* Clicked Restart Now
* Pressed Enter when told to remove the USB media (unless you set it to boot from USB first, instead of just selecting it one-time from the BIOS boot override options or the F8 menu, this is fine)
* After restarting, the machine seemed to have hung, with a blank screen and no activity from the disk activity LED, so I tried just typing the disk encryption password and pressing Enter, which seemed to work. Given this also happened with elementary OS, another Ubuntu derivative, I am assuming it is something to do with Ubuntu, or the device’s framebuffer before the graphics driver is loaded.
* Waited a while for the system to boot, typed my login password and pressed Enter
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Driver Manager
* It said "You appear to be offline. Connect to the internet or insert the Linux Mint installation disc (or USB stick)." so I clicked OK, nothing changed, so I removed and re-inserted it, and clicked OK again.
* Clicked Mount installation media in the Driver Manager window and entered my password
* Selected broadcom-sta-dkms and clicked Apply Changes and entered my password
* Clicked Restart (you can avoid this if you want to, by using `rmmod` to remove conflicting modules (`b43`, `b43legacy`, `b44`, `bcma`, `brcm80211`, `brcmsmac` and `ssb`), and `modprobe` to load the `wl` module now it is installed (you may also need `cfg80211`, but restarting is easier to describe)
* Again, after restarting, the machine seemed to have hung, with a blank screen and no activity from the disk activity LED, so I tried just typing the disk encryption password and pressing Enter
* Entered my password and pressed Enter again to log in
* Checked the WiFi network was connected (credentials were copied from the live environment)
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Update Manager, and clicked OK in the Update Manager, then Apply the Update to update it, and entered my password
* Opened Settings, clicked on Languages, clicked Apply System-Wide, and entered my password
* The Update Manager still hadn't loaded available updates, so I closed it and reopened it
* I clicked Install Updates in the Update Manager to install all available updates and entered my password again
* Although it isn't required, I rebooted, since there was a kernel update, and I left the machine overnight to see if a disk encryption password prompt would appear (it didn't, but entering the password worked), obviously logging in again after the reboot
* Launched the firewall configuration tool, entered my password, and enabled it
* Removed the install USB key, since it didn't seem to be detected/mounted (possibly related to leaving the system overnight waiting for a password prompt)
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd), and entered my password
* Opened the firewall configuration utility from the LM Menu, Preferences, Firewall Configuration, and entered my password
* Clicked the Rules tab, clicked the plus button, set Policy: Allow, Direction: In, Category: Network, Subcategory: Services, Application: SSH, and clicked Add, and closed the add window. This isn't particularly secure, and you should probably limit it to the local network, if you are going to use untrusted networks, and configure sshd to accept only SSH keys, if the security of the system matters.
* Checked I could login by getting the IP address with `ip addr` in the terminal and then running `ssh 192.168.1.197` (obviously put the actual LAN IP address from `ip addr`) on another machine, and pressing Ctrl-D to logout
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling the firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks

## Linux Mint MATE Edition 22.2

MATE is perhaps less easy to use than Cinnamon, but I'm not sure, and I disliked the Linux Mint implementation, but it has a longer history (since it is a continuation of GNOME 2), and maybe possibly less resource intensive? I suggest Cinnamon to new users on Linux, but I wanted to try this as I've never used MATE before, and was curious how it compared on Linux Mint to Xfce and Cinnamon. I think that Linux Mint customises all the desktops it supports to be similar though (at least Xfce was unlike the default Xfce).

I used the following image for this (sha256sum): `21f5a5f7be652c60b20ba7996328098b14e979b1ef8bf7f6c9d4a2a579504a65  linuxmint-22.2-mate-64bit.iso`

* Selected Start Linux Mint from the GRUB menu
* Ignored various errors/messages from the kernel/boot sequence and waited for the desktop to appear
* Clicked the LM menu button, All Applications, Administration, Driver Manager
* Waited for it to scan for drivers
* Selected the broadcom-sta-dkms option, and clicked Apply Changes
* Closed Driver Manager
* Clicked on the network settings icon (showing no connection, a pair of arrows with a cross) on the bottom right of the screen in the notification area
* Clicked on my WiFi network SSID under Available networks, and entered the key and pressed Enter
* Checked the internet was working by opening Firefox and navigating to <https://bbc.co.uk/>
* Double clicked the Install Linux Mint desktop icon
* Clicked Continue with English selected as the language
* Clicked on the English (UK) keyboard layout category and then clicked Continue with the English (UK) variant selected
* Selected Install multimedia codecs and clicked Continue
* Selected Erase disk and install Linux Mint, didn't select any advanced features, (different wording may be present if it doesn't detect another OS) then clicked Install Now
* Clicked Continue on the confirmation box about partitioning
* Clicked Continue with London selected as my location
* Entered my name as `Nick Cripps` (obviously enter your own name, bearing in mind it will be shown on the login screen in full), computer name as `pyros` (this is what I have chosen for this device, choose something else if you are following this, but use lowercase), `sipos` as username (again, choose something different if you are not me, this is what I use for obscure reasons), entered a password and confirmed it, left Require my password to log in checked (you may wish to disable this if you use disk encryption and do not plan to leave the system unattended while powered, or are using it where a password is unnecessary), and left Encrypt my home folder unchecked (use full disk encryption for greater security, unless you share the computer with someone else you want privacy from) and clicked Continue
* Waited a while for installation to complete
* Clicked Restart Now
* Pressed Enter when told to remove the USB media (unless you set it to boot from USB first, instead of just selecting it one-time from the BIOS boot override options or the F8 menu, this is fine)
* Waited a while for the system to boot, typed my login password and pressed Enter
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Driver Manager
* Clicked Mount installation media in the Driver Manager window and entered my password
* Selected broadcom-sta-dkms and clicked Apply Changes and entered my password
* Clicked Restart (you can avoid this if you want to, by using `rmmod` to remove conflicting modules (`b43`, `b43legacy`, `b44`, `bcma`, `brcm80211`, `brcmsmac` and `ssb`), and `modprobe` to load the `wl` module now it is installed (you may also need `cfg80211`, but restarting is easier to describe)
* Entered my password and pressed Enter again to log in
* Checked the WiFi network was connected (credentials were copied from the live environment)
* Clicked Let's go! on the Welcome window
* Clicked Launch for the Update Manager, and clicked OK in the Update Manager, then Apply the Update to update it, and entered my password
* Right clicked the Linux Mint 22.2 MATE 64-bit USB key icon on the desktop and clicked Eject, then removed the drive when the notification saying it was safe to do so appeared
* I clicked Install Updates in the Update Manager to install all available updates and entered my password again
* Opened Control Centre, clicked on Languages, clicked Apply System-Wide, and entered my password
* Although it isn't required (though an orange box briefly said it was before disappearing), I rebooted, since there was a kernel update, obviously logging in after the reboot
* Launched the firewall configuration tool, entered my password, and enabled it
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd), and entered my password
* Opened the firewall configuration utility from the LM Menu, All Applications, Preferences, Firewall Configuration, and entered my password
* Clicked the Rules tab, clicked the plus button, set Policy: Allow, Direction: In, Category: Network, Subcategory: Services, Application: SSH, and clicked Add, and closed the add window. This isn't particularly secure, and you should probably limit it to the local network, if you are going to use untrusted networks, and configure sshd to accept only SSH keys, if the security of the system matters.
* Checked I could login by getting the IP address with `ip addr` in the terminal and then running `ssh 192.168.1.197` (obviously put the actual LAN IP address from `ip addr`) on another machine, and pressing Ctrl-D to logout
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling the firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks

## MX Linux Xfce x64 23.6

This seems like a nice live system or distro for a bit more experienced users, and a good system for RAM constrained systems. It feels a little less flexible than default Xfce, but perhaps a bit more overall polished for desktop use than Xfce on Debian or Gentoo. It includes and activates the `wl` proprietary WiFi driver automatically. It has some nice tools to do common tasks easily with a GUI, and great tools to create a bootable live system backup, and does not use systemd by default. It is a little less command-line based than I would like though. I would switch to this if I didn't like Gentoo so much, but I'd recommend Linux Mint Cinnamon Edition to new users. I disliked that updates took ages to generate loads of locales I am not using, but this is easily fixed. I tried reinstalling, and rebooting a couple of times, with full disk encryption, and that seemed to work fine too.

I used the following image for this (sha256sum): `6960a253320a7615217b07593fcd04f7ab6126a87cce1398e2c153c45ca03978  MX-23.6_x64.iso`

* Pressed enter in syslinux boot menu on MX-23.6 x64 (April 13 2025)
* Waited for boot, ignoring kernel messages
* Clicked on the disconnected Ethernet icon on the left, and clicked on my WiFi network under Available Networks, clicked in the key text box, entered the key and pressed Enter
* Clicked on the MX User Manual icon on the desktop, then closed the PDF viewer and user manual PDF file it opened
* Clicked on the Firefox icon and navigated to <https://bbc.co.uk/> to check internet connectivity was working, then closed Firefox
* Clicked on Install MX Linux on the MX Welcome window
* Waited for the installation media check to finish
* Clicked Change Keyboard Settings, clicked the plus button, Selected English (UK) from the Layout menu, left the variant menu on No Variant, clicked OK, and then clicked on the us English (US) entry, clicked the minus button, clicked OK, clicked Next
* Selected Regular install using the entire disk, left the disk menu on sda (59,6 GB GPT - FORESEE 64GB SSD), left the root/home space slider at 100% for root, left Encrypt unselected, and checked Enable hibernation support, and clicked Next
* Clicked Start on the confirmation page
* Changed the computer name to `pyros` (this is what I am naming this device, choose your own hostname if you follow this), the computer domain to `0point.cc` (this is my domain, use your own or leave it if you are following this), unselected SaMBa Server for MS Networking, and clicked Next
* Changed localization defaults to United Kingdom - British English, the timezone to Europe and London, left system clock uses local time unchecked, left the format as 13:57, clicked view on Service Settings, but then Back, and then clicked Next
* Entered `sipos` (this, for obscure reasons, is the username I use, choose your own if following this) for default user login name, entered and confirmed a password for the default user, left the Root (administrator) Account checkbox unchecked, left the Autologin and Save live desktop changes checkboxes unchecked, and clicked Next
* Waited for the install to finish
* Left Automatically reboot he system when the installer is closed checked, and clicked on Finish
* Waited for the system to reboot, entered my password, and pressed Enter
* The WiFi network auto-connected, thanks to the config being copied from the live environment
* Clicked on the green box icon	in the notification area, ran a full upgrade, entered my password, pressed y and enter to accept, waited for update to complete (which took ages, especially generating unneeded locales), (did the next two points while waiting), pressed enter to close
* I tested each of the options from the MX Welcome screen, and the MX Tools window, but didn't change any settings, then closed it
* Clicked on the eject icon in the notification area, but no removable media was show, so I opened the file manager, which showed the MX-Live USB under Devices with an eject icon, so I clicked it, and removed the live USB when it said it was safe to do so
* I noticed that my full name wasn't asked for, so not set in `/etc/passwd`, so I updated it with mugshot
* Since updates included changes to initrd and kernel I think, I rebooted, and logged-in with my password
* Opened MX Package Installer, and added GIMP Full and Inkscape from Graphics, and GB_English_Firefox, GB_English_Libreoffice and GB_English_Thunderbird from Language, and clicked Install, entered my password, waited for the install to happen, clicked OK to confirm installation of the list of packages and deps, entered y and pressed Enter to install, clicked OK on the dialogue saying it had finished, and close
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd), and entered my password
* Rebooted (not necessary)
* Opened the firewall configuration utility from the MX Menu, Settings, Firewall Configuration, and entered my password
* Clicked the Rules tab, clicked the plus button, set Policy: Allow, Direction: In, Category: Network, Subcategory: Services, Application: SSH, and clicked Add, and closed the add window. This isn't particularly secure, and you should probably limit it to the local network, if you are going to use untrusted networks, and configure sshd to accept only SSH keys, if the security of the system matters.
* Checked I could login by getting the IP address with `ip addr` in the terminal and then running `ssh 192.168.1.197` (obviously put the actual LAN IP address from `ip addr`) on another machine, and pressing Ctrl-D to logout
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling a firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks

I tried PyCharm and CLion, downloaded as tgz files, from the JetBrains website, as well, on my second install that had FDE. All seems fine.

I also tested suspend, which works and puts the system in standby, there is no hibernate option, presumably because it is kind of unnecessary. I did have to enable the lock screen in Xfce screensaver settings to get the screen to lock on suspend, and had to turn off the on-screen keyboard to get rid of it. Mouse movements wake the system by default, which is probably undesirable, but this is basically a laptop system - not much power consumption and silent.

## MX Linux Xfce AHS x64 23.6

I didn't notice a difference with the above (the non-AHS version), but I didn't look closely at what was supported or not or performance etc.

I used the following image for this (sha256sum): `fe830d95bf124cb8feb26f92ad1934acf3762fb540167c4db4dffee2c40c756f  MX-23.6_ahs_x64.iso`

* Pressed enter in syslinux boot menu on MX-23.6 ahs x64 (April 13 2025)
* Waited for boot, ignoring kernel messages
* Clicked on the disconnected Ethernet icon on the left, and clicked on my WiFi network under Available Networks, clicked in the key text box, entered the key and pressed Enter
* Clicked on the Firefox icon and navigated to <https://bbc.co.uk/> to check internet connectivity was working, then closed Firefox
* Clicked on Install MX Linux on the MX Welcome window
* Waited for the installation media check to finish
* Clicked Change Keyboard Settings, clicked the plus button, Selected English (UK) from the Layout menu, left the variant menu on No Variant, clicked OK, and then clicked on the us English (US) entry, clicked the minus button, clicked OK, clicked Next
* Selected Regular install using the entire disk, left the disk menu on sda (59,6 GB GPT - FORESEE 64GB SSD), left the root/home space slider at 100% for root, checked Encrypt and Enable hibernation support, and clicked Next
* Entered and confirmed an encryption password, and clicked Next
* Clicked Start on the confirmation page
* Changed the computer name to `pyros` (this is what I am naming this device, choose your own hostname if you follow this), the computer domain to `0point.cc` (this is my domain, use your own or leave it if you are following this), unselected SaMBa Server for MS Networking, and clicked Next
* Changed localization defaults to United Kingdom - British English, the timezone to Europe and London, left system clock uses local time unchecked, left the format as 13:57, clicked view on Service Settings, but then Back, and then clicked Next
* Entered `sipos` (this, for obscure reasons, is the username I use, choose your own if following this) for default user login name, entered and confirmed a password for the default user, left the Root (administrator) Account checkbox unchecked, left the Autologin and Save live desktop changes checkboxes unchecked, and clicked Next
* Waited for the install to finish
* Left Automatically reboot he system when the installer is closed checked, and clicked on Finish
* Waited for the system to reboot, entered the disk encryption password and pressed Enter, entered my password and pressed Enter
* The WiFi network auto-connected, thanks to the config being copied from the live environment
* Right clicked on the box icon in the notification area, and selected Check for updates
* Clicked on the green box icon	in the notification area, ran a full upgrade, entered my password, pressed y and enter to accept, waited for update to complete (which took ages, especially generating unneeded locales), (did the next two points while waiting), pressed enter to close
* Clicked on the eject icon in the notification area, but no removable media was show, so I opened the file manager, which showed the MX-Live USB under Devices with an eject icon, so I clicked it, and removed the live USB when it said it was safe to do so
* I noticed that my full name wasn't asked for, so not set in `/etc/passwd`, so I updated it with mugshot
* The package update process said that a config file (`/etc/X11/Xsession.d/98vboxadd-xclient`) was modified by me or a script since installation, and asked whether I want the package maintainer's version, the currently-installed version, to show the differences or start a shell, so I pressed d Enter to see the differences, the newer version seemed better, so I pressed q to exit less with the diff, y and Enter to accept the package maintainer's (new) version.
* Pressed a key to close the package update window.
* Since updates included changes to initrd and kernel I think, I rebooted, and logged-in with my password
* Opened MX Package Installer, and added GIMP Full and Inkscape from Graphics, and GB_English_Firefox, GB_English_Libreoffice and GB_English_Thunderbird from Language, and clicked Install, entered my password, waited for the install to happen, clicked OK to confirm installation of the list of packages and deps, entered y and pressed Enter to install, clicked OK on the dialogue saying it had finished, and close
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git openssh-server` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd), and entered my password
* Rebooted (not necessary), entered the disk encryption password, pressed Enter, entered my password, pressed Enter
* Opened the firewall configuration utility from the MX Menu, Settings, Firewall Configuration, and entered my password
* Clicked the Rules tab, clicked the plus button, set Policy: Allow, Direction: In, Category: Network, Subcategory: Services, Application: SSH, and clicked Add, and closed the add window. This isn't particularly secure, and you should probably limit it to the local network, if you are going to use untrusted networks, and configure sshd to accept only SSH keys, if the security of the system matters.
* Checked I could login by getting the IP address with `ip addr` in the terminal and then running `ssh 192.168.1.197` (obviously put the actual LAN IP address from `ip addr`) on another machine, and pressing Ctrl-D to logout
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling a firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks

# Debian 13.1.0 (trixie) x64

Debian is a good solid distribution that has been around for ages, and values software freedom. It perhaps isn't the easiest for new users though. It is what everything else described here, except Gentoo, is based on though.

I installed this with Ethernet connected as I know from experience that the driver for WiFi on this machine isn't available in the Debian install environment.

It isn't hard to automate Debian installation. TODO: add link to my repo for that

I used the following image for this (sha256sum): `658b28e209b578fe788ec5867deebae57b6aac5fce3692bbb116bab9c65568b3  debian-13.1.0-amd64-netinst.iso`

* Pressed Enter on Graphical install in the GRUB menu
* Ignored kernel ACPI error messages
* Clicked Continue with English selected
* Selected United Kingdom and clicked Continue
* Clicked Continue with British English highlighted for the keyboard
* Waited for the install media to be detected and mounted, and components loaded
* Waited for the network to autoconfigure
* Entered `pyros` for the hostname (this is what I am naming this device, choose your own hostname if you follow this) and clicked Continue
* Entered `0point.cc` for the domain name (this is my domain, use your own or leave it if you are following this) and clicked Continue
* Entered and confirmed a root password, and clicked Continue
* Entered my name, `Nick Cripps` for the full name of the new user (obviously enter your own if you are following this) and clicked Continue
* Entered `sipos` for the username (this, for obscure reasons, is the username I use, choose your own if following this) and clicked Continue
* Entered and confirmed a password and clicked Continue
* Waited for steps to finish
* Selected Guided - use entire disk and clicked Continue
* Left the SCSI1 (0,0,0) (sda) - 64.0 GB ATA FORESEE 64GB SSD entry selected, and clicked Continue
* Left All files in one partition (recommended for new users) selected and clicked Continue
* Clicked Continue with Finish partitioning and write changes to disk selected still
* Selected Yes to write changes to disk and clicked Continue
* Waited for installation to proceed
* Left United Kingdom selected for the mirror location, and clicked Continue
* Left deb.debian.org selected and clicked Continue
* Clicked Continue with nothing entered for HTTP proxy
* Waited for the package manager configuration to proceed and software list to be retrieved
* Left No selected for participation in package popularity contest (this isn't a typical install) and clicked Continue
* Left Debian desktop environment checked, unchecked GNOME, checked Xfce, left GNONE Flashback, KDE Plasma, Cinnamon, MATE, LXDE and LXQt unchecked, left web server unchecked, checked SSH server, left standard system utilities checked and Choose a Debian Blend for installation unchecked, and clicked Continue
* Waited for packages to be retrieved and installed
* Left Yes selected for Install GRUB boot loader to your primary drive, and clicked Continue
* Selected /dev/sda (ata-FORESEE_64GB_SSD_F36237R00073) and clicked Continue
* Clicked Continue to reboot
* Ignored kernel ACPI and wireless driver error messages, and other messages
* Entered my username and password
* Right-clicked the `Debian 13.1.0 amd64 n` volume on the desktop, and selected Safely Remove Volume and removed the installation USB key
* Opened a terminal from the icon at the bottom of the screen
* Ran `su -` and entered the root password to get a root shell, ran `gpasswd -a sipos sudo`, pressed Ctrl-D to end the root shell, and again to end the user shell, then logged out and back in again
* Opened a terminal and ran `sudo -e /etc/apt/sources.list` and added ` non-free` to the end of the `deb http://deb.debian.org/debian/ trixie main non-free-firmware` and saved and exited with Ctrl-X, y, Enter
* Ran `sudo apt update`, if it reports any out of date packages, run `sudo apt upgrade -y`, but it didn't for, me so I didn't
* Ran `sudo apt install -y linux-headers-$(uname -r | sed 's,[^-]*-[^-]*-,,') broadcom-sta-dkms` and then rebooted (you can avoid the restart if you want to, by using `rmmod` to remove conflicting modules (`b43`, `b43legacy`, `b44`, `bcma`, `brcm80211`, `brcmsmac` and `ssb`), and `modprobe` to load the `wl` module now it is installed (you may also need `cfg80211`, but restarting is easier to describe)
* Entered my username and password
* Clicked on the network cable icon in the notification are on the top right, and clicked on my WiFi network SSID under Available networks
* Clicked in the WiFi key box, entered my WiFi key and pressed Enter
* Disconnected the Ethernet cable
* Opened the terminal and ran `sudo apt install -y build-essential python3 python3-virtualenv git` (to install a C/C++ compiler, make, python3 virtualenv, git and sshd), and entered my password
* Ran `sudo apt install -y ufw`, then `sudo ufw enable && sudo ufw default deny incoming && sudo ufw default allow outgoing && sudo ufw allow ssh`
* Checked I could login by getting the IP address with `ip addr` in the terminal and then running `ssh 192.168.1.197` (obviously put the actual LAN IP address from `ip addr`) on another machine, and pressing Ctrl-D to logout
* Signing-in to Firefox to share bookmarks, passwords, settings, etc, probably makes sense
* Backing up files somewhere off-site obviously makes sense too
* Enabling a firewall if you are using the device outside your home network or other trusted networks would be sensible too, disabling the SSH rule above, or changing profile, before connecting to untrusted networks
