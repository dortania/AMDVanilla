# Final touches

## We're done! ~~\(or are we?\)~~

### Booting macOS

Now that our macOS install is fully set up for AMD computers we can finally boot in to it. Reboot your computer one last time and from clover select the option _Boot macOS from macOS._

You probably notice that some things are wrong...

### Installing clover to your drive

As of now you cannot boot macOS without your USB drive.

We will need to fix that, as nobody wants to keep a USB drive plugged in at all times.

Install Clover as described in **Preparing the installer**, except this time select your drive as the destination, not your USB. A drive named EFI will appear on your desktop once again. We will need to copy your config and kexts there. But you may notice that the EFI of our USB drive is no longer shown! You will have to mount that yourself, as macOS does not do that by default. To do so run the following commands from a _Terminal_ window:

```bash
diskutil list
```

This will list all the available disks and their partitions. From that wall of text we have to find out what identifier our EFI has. You will have to look for the following things:

* /dev/disk_x_ \(external, physical\)  This indicates an external drive, like our USB drive
* A partition of the type EFI with the name EFI This is the partition we are looking for! Note the identifier that is written next to it.

We can now mount our EFI, you can do that as follows:

```text
sudo diskutil mount disk(x)s(x)
```

Change the x's to be the same as in your identifier.

You will be prompted to enter your password, and after that a drive named EFI will pop up on your desktop.

Now from this EFI on your USB drive copy the following files and directories to the EFI of your drive:

* kexts/
* config.plist

With this done Clover is installed to your HDD and you will no longer need your HDD to boot!

### Installing Nvidia drivers

If you are on any decently modern Nvidia card you will notice that things are running slowly, and when you open up _About this mac_ the wrong graphics card is shown, or has the wrong amount of VRAM. This is because Nvidia cards now require WebDrivers to work properly. These work exactly like drivers on Windows, but are a bit more picky with their requirements. You need to download the drivers for exactly your macOS version, including build. To get your build number do the following:

1. Press the Apple in the top left corner
2. Click on _About this mac_
3. A window will pop up
4. In this window press on _Version 10.13.x_. 
5. The build version will show next to it.

You can use [this useful guide](https://www.insanelymac.com/forum/topic/324195-nvidia-web-driver-updates-for-macos-high-sierra-update-december-7-2018/) made by fantomas1 over on InsanelyMac to download the version needed for your specific macOS version.

### Fixing Ryzen sound

You may have noticed that you don't have sound on your Ryzen system. This can be fixed by following [the following guide](https://forum.amd-osx.com/viewtopic.php?f=24&t=4880) over at AMD OS X.

**Use the** _**Semi**_**-Automated setup!**

### **Fixing Ryzen USB**

Currently you are probably using GenericUSBXHCI.kext for USB support on your Ryzen system, but that is not needed and can cause instabilities and even kernel panics! Ryzen USB has native support from macOS! This is shown on the following page.

### VoodooTSCSync

This kext syncs the TSC, improving sync for time, audio and video.

Download it here, and install it as follows:

Open _Terminal_ and run the following command

```bash
echo $(($(sysctl -n hw.ncpu) - 1))
```

Note down 
