# Installing

Congratulations, you have made your installer!  
Now how do you install with it?

## BIOS

For the best results you should set your BIOS to the following settings:

* Execute Virtual Bit: Enabled 
* Secure Virtual Machine\(SVM\): Disabled \(Enable if needed, but untested and may lead to issues.\)
* Cool 'n Quiet = Enabled 
* **APU = Disabled \(May also be denoted as** _**Integrated Graphics**_**\)**
* Spread Spectrum = Auto 
* Serial & Parallel = Disabled 
* HPER = Enabled 
* **EHCI Handoff = Enabled** 
* **XHCI Handoff = Enabled** 
* _**Sata Mode = AHCI**_ 
* IDE = Disabled 
* **IOMMU = Disabled**
* HPC = Enabled

The settings denoted in bold and italic are absolutely required, as without them basic functionality such as HDD access will not be available.

Settings in bold are highly recommended though you may experience issues with them set incorrectly.

All other settings are best set as advised, but are not crucial.

\***Make sure you have Legacy disabled. If your machine is not set to be UEFI only you may experience issues!\***

## Booting the installer

### First boot

When you first boot your computer you will be prompted with the Clover screen. Chose the _OS X Base System_ entry. When this is finally booted you will be greeted by a screen to chose your language. Do just that and a menu of options will be shown.

### Drive setup

We will need to setup our HDD/SSD first before we can install macOS on it.

You will need to launch the option called _Disk Utility_. You will be greeted by the following screen:

Chose the drive you want to install macOS to and press _Erase_ from the top bar.

A popup will appear with 3 fields. In the first one you enter the name you want your drive to have. I am naming mine "macOS", and so all the commands used further on in this guide will be for a drive named "macOS". For _Format_ I recommend choosing _Mac OS Extended \(Journaled\)_ for an HDD and _APFS_ for an SSD. Make sure _Scheme_ is set to GUID Partition Map

_**NOW MAKE SURE THAT ALL THE DATA ON THIS DRIVE IS BACKED UP AND THAT YOU HAVE SELECTED THE CORRECT DRIVE!! WE ARE ABOUT TO ERASE IT!**_

Now press _Erase_ and our disk setup is completed!

### First phase of install

Now that our drive has been set up you can exit disk utility and launch _Reinstall macOS_ and hit _Continue._ When you are prompted to select what drive you want to install to select your previously configured drive, in my case "macOS". This part of the installer does not actually install the OS, but only copies the files needed to do so to the drive.

When this part is done the installer will automatically reboot.

### Pre-Install modification

During the previous phase of the install a prelinkedkernel was copied over to the drive. This is the default prelinkedkernel containing the native Intel kernel, and thus cannot be booted by our AMD system. We will have to replace it.

To do so boot back in to the _OS X Base System_, in Clover, instead of what is automatically selected. Wait for the installer to boot again, chose your language and you will again be prompted by the window with multiple choices. This time we won't be using those.

On the bar on top of your screen press _Utilities_ and from the dropdown menu that shows up launch _Terminal_. Now enter the following command to copy the prelinkedkernel from our USB to the installer on the drive.

```bash
cp -Rf /System/Library/PrelinkedKernels/prelinkedkernel /Volumes/macOS/macOS\ Install\ Data/Locked\ Files/Boot\ Files/prelinkedkernel
```

You will also need to modify a plist to remove `auth-g` so the prelinkedkernel will boot.

```bash
sed -i '' 's/auth-//g' /Volumes/macOS/macOS\ Install\ Data/Locked\ Files/Boot\ Files/com.apple.Boot.plist
```

You can now reboot your computer by typing

```bash
reboot
```

### Installing macOS

Once your computer reboots and you are back in Clover select the option named _Boot macOS Install from macOS_. This will launch the installer. This process takes a while.

### Post-Install modifications

When the system boots back up macOS will be installed, but it will be using the default prelinkedkernel and kernel, making it unbootable on AMD systems. Because of that we need to copy over some files.

First launch _Terminal_ as instructed previously in **Pre-Install modification**. From here we will be executing a few commands. First the most important: Copying the kernel.

```bash
cp -Rf /System/Library/Kernels/kernel /Volumes/macOS/System/Library/Kernels/kernel
```

#### Ryzen Instructions

Now that the kernel has been copied you are almost done on Ryzen. You will need to copy over two kexts and then you will only have to rebuild the prelinkedkernel aka kextcache. This is done in the same way as when we were setting up the USB drive.

```bash
cp -rf /System/Library/Extensions/IONetworkingFamily.kext /Volumes/macOS/System/Library/Extensions/IONetworkingFamily.kext
cp -rf /System/Library/Extensions/System.kext /Volumes/macOS/System/Library/Extensions/System.kext
chown -R 0:0 /Volumes/macOS/System/Library/Extensions
chmod -R 755 /Volumes/macOS/System/Library/Extensions/*.kext
touch /Volumes/macOS/System/Library/Extensions

rm -rf /Volumes/macOS/System/Library/PrelinkedKernels/prelinkedkernel
kextcache -u /Volumes/macOS
```

Again we first delete the old prelinkedkernel just in case, and with the second command we rebuild the kextcache on the _macOS_ volume. Once again it will probably spit out a lot of text, but so long as you get the cache ID in the end the rebuild succeeded.

#### FX Instructions

If you are on FX and have used the aforementioned DummyUSB kexts you will need to copy them over to the new install, you will also need to copy the IONetworking and System kexts. You can do that with the following command:

```bash
cp -rf /System/Library/Extensions/Dummy*.kext /Volumes/macOS/System/Library/Extensions/
cp -rf /System/Library/Extensions/IONetworkingFamily.kext /Volumes/macOS/System/Library/Extensions/IONetworkingFamily.kext
cp -rf /System/Library/Extensions/System.kext /Volumes/macOS/System/Library/Extensions/System.kext
```

Since we are adding kexts to S/L/E we will have to fix their permissions. This is done just like before with the following commands:

```bash
cd /Volumes/macOS/System/Library/
chown -R 0:0 Extensions
chmod -R 755 Extensions/*.kext
touch Extensions
```

Now we can finally rebuild our prelinkedkernel. This is done in the same way as when we were setting up the USB drive.

```bash
rm -rf /Volumes/macOS/System/Library/PrelinkedKernels/prelinkedkernel
kextcache -u /Volumes/macOS
```

Again we first delete the old prelinkedkernel just in case, and with the second command we rebuild the kextcache on the _macOS_ volume. Once again it will probably spit out a lot of text, but so long as you get the cache ID in the end the rebuild succeeded.

### After installing

Set up macOS to your liking, but do not sign in to your Apple ID when prompted. You can do this later in the settings.

