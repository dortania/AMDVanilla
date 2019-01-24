# Preparing the installer

### Copying the kernel

macOS will not be able to boot on AMD systems in this configuration. For that to work we need to replace a few files.

The new Kernel will need to be placed in the _System/Library/Kernels_ folder of the installer USB. This folder does not exist by default, so you need to go to _System/Library_ and create the folder _Kernels_.

```bash
diskutil mount /dev/disk#s#
cd /Volumes/OS\ X\ Base\ System/System/Library
mkdir Kernels
cp ~/Desktop/kernel Kernels/kernel
sudo cp -r ~/Desktop/System.kext Extensions/System.kext
sudo cp -r ~/Desktop/IONetworkingFamily.kext Extensions/IONetworkingFamily.kext
```

The first command mounts the USB drive.  
The second command changes the current directory to the USB drive's _System/Library_  
The third command creates the _Kernels_ directory  
The fourth command copies the kernel from the desktop  
The fifth and sixth commands copy _System.kext_ and _IONetworkingFamily.kext_ from the desktop

### Copying some kexts

The BaseSystem image needs some kexts to be replaced to boot macOS on AMD. We will have to add these.

Extract the .ZIP with kexts that you downloaded to your desktop.

You will also need the following files for USB support.

* DummyUSBEHCIPCI.kext
* DummyUSBXHCIPCI.kext

These files can be downloaded [here](https://github.com/hackintosh-guides/AMDVanilla/tree/master/files). We do not need them on Ryzen as we will be setting up native USB. This will be explained later on.

#### Side note:

Do not add your other kexts here. We will add those later to Clover.

Extract the Zip file to your desktop to a folder named kexts. After that open _Terminal_ and run the following command to copy the needed files.

```bash
cp -r ~/Desktop/kexts/. Extensions/
```

### Rebuilding the prelinkedkernel

macOS does not use the kernel file to boot. Instead it uses the prelinkedkernel. This is a file containing the Kernel along with a cache of kexts. Because of this in order to be able to boot we need to rebuild it. First we will have to rebuild the permissions.

Open a Finder window and right click on your USB drive. Press `Get Info`. On the very bottom of the window that just opened press on the lock and enter your password to unlock some extra settings. Now uncheck `Ignore Ownership` from the now no longer greyed out options at the bottom of the page.

Now that this is done, open a terminal window again and execute the following commands:

```bash
cd /Volumes/OS\ X\ Base\ System/System/Library/
sudo chown -R 0:0 Extensions
sudo chmod -R 755 Extensions/*.kext
sudo xattr -c Extensions/*
sudo touch Extensions
sudo rm /Volumes/OS\ X\ Base\ System/System/Library/PrelinkedKernels/prelinkedkernel
sudo kextcache -u /Volumes/OS\ X\ Base\ System
```

This process can take a few minutes and when it is done you will most likely receive an error complaining about `com.apple.kext.caches/Startup`; as long as you also receive a Cache ID this is fine.

The first 5 commands are used to repair permissions on the kexts. The first command changes directory to the `Library`folder. The second one changes the owner of all files in the `Extensions` folder to root.The third one changes the permissions of all kexts in the `Extensions` folder so that the file owner has full control. The command after that strips all extra attributes the files might have. The last of this section of commands basically updates the modification date of all files in the `Extensions` folder.

The last two commands are used to rebuild the prelinkedkernel. The first one removes the existing file and the second one is what rebuilds the kernel cache aka the prelinkedkernel.

### Installing Clover

For this next part we will be installing the bootloader _Clover_ to the USB drive so that it can be booted on regular computers, not just Macs.  
Let's get started.

Launch your Clover installer that you downloaded in the prerequisites section. On the second page of the installer **make sure to select your USB drive!** The default settings set by Clover are not all that desirable so we need to **Customise** the install.

You want to use the following settings, as shown in the screenshots. This is generally all that's needed.

* _Install Clover for UEFI booting only_
* _Install Clover to the ESP_
* Under _Drivers64UEFI:_
  * _AptioMemoryFix_ \(the new hotness that includes NVRAM fixes, as well as better memory management\)
  * _VBoxHfs-64.efi_ \(or _HFSPlus.efi_ if available\) - one of these is required for Clover to see and boot HFS+ volumes. If you see the option to enable it in the installer, make sure it's selected - if you don't see it in the installer, verify that one of them exists in the _EFI -&gt; CLOVER -&gt; drivers64UEFI_ folder
  * _ApfsDriverLoader_ - \(Available in Dids' Clover builds - or [here](https://github.com/acidanthera/ApfsSupportPkg/releases)\) this allows Clover to see and boot from APFS volumes by loading apfs.efi from ApfsContainer located on block device \(if using AptioMemoryFix as well, requires R21 or newer\)
* _Install RC scripts on target volume_

Provided you don't plan on using FileVault \(which I don't even think works properly on AMD\) this concludes our Clover installation!

### Copying kexts

When Clover is done installing a drive named EFI will pop up on your desktop. Open this and navigate to _/Volumes/EFI/EFI/CLOVER/kexts/Other_ and copy all your .kext files that you downloaded in the Kexts section here.

You will also see other folders named 10.xx in the _/kexts/_ directory. These are not needed for our goal. These are used for version specific kexts in case you are multibooting multiple macOS versions.

## Next up:

### Setting up Clover

First some theory on how it all works, and after that I will show a few different configs that should work as a basis for most systems. Follow the guide for your CPU on the left side under the heading "_Example Config.plists"_, after reading the basics.

