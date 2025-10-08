# Other Linux Distros I Tried on the Promethean ActiveConnect

## Linux Mint Cinnamon Edition 22.2

See [README.md](README.md#linux-mint-cinnamon-edition-22.2).

## Ubuntu 24.04.3 LTS (Noble Numbat)

See [README.md](README.md#ubuntu-24.04.3-lts-noble-numbat).

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
