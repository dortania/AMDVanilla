# Final touches

## We're done! ~~\(or are we?\)~~

### Booting macOS

Now that our macOS install is fully set up for AMD computers we can finally boot in to it. Reboot your computer one last time and from clover select the option _Boot macOS from macOS._

You probably notice that some things are wrong...

### Installing Clover to your drive

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
* ACPI/patched/DSDT.aml
* config.plist

With this done Clover is installed to your HDD and you will no longer need your HDD to boot!

### Fixing Ryzen sound

You may have noticed that you don't have sound on your Ryzen system. This can be fixed by following [the following guide](https://forum.amd-osx.com/viewtopic.php?f=24&t=4880) over at AMD OS X.

**Use the** _**Semi**_**-Automated setup!**

### VoodooTSCSync

This kext syncs the TSC, improving sync for time, audio and video.

[Download it here,](https://github.com/IOIIIO/AMDVanilla/raw/master/files/VoodooTSCSyncAMD.zip) and install it as follows:

Open _Terminal_ and run the following command

```bash
echo $(($(sysctl -n hw.ncpu) - 1))
```

Note down the response.

Right click on VoodooTSCSync.kext and select _Show package contents_. When that is done navigate to Contents and open Info.plist. I recommend the free piece of software _Textwrangler_ for this. Find line 36 or just search for `#CORE`. The line above it should say `<key>IOCPUNumber</key>`. Now change \#CORE with the number you got before. Save the changes, and add the kext to your EFI's kexts/Other.

