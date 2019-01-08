# Kexts

## What kexts do you need?

### The kext that is absolutely required

_VirtualSMC.kext_ \(or _FakeSMC.kext_\) is as aforementioned essential. This kext is what tells macOS "Yes this is a real mac", emulating the functionality of the SMC on real Macs \(hence the name\). Without it, no Hackintosh.

### Where can I find these kexts?

All the kexts shown here are available for download on the [_**kext repo**_](https://1drv.ms/f/s!AiP7m5LaOED-m-J8-MLJGnOgAqnjGw) provided and maintained by Goldfish64. All these kexts are automagically built when a new kext update is commited.

### Ethernet

* _​_[_IntelMausiEthernet.kext_](https://github.com/Mieze/IntelMausiEthernet) - this works with most newer Intel LAN chipsets
* [_AppleIntelE1000e.kext_](https://sourceforge.net/projects/osx86drivers/) - this works with older Intel LAN chipsets - but can cause KPs on newer chipsets
* _​_[_AtherosE2200Ethernet.kext_](https://github.com/Mieze/AtherosE2200Ethernet) - this works for most Atheros or Killer networking chipsets
* _​_[_RealtekRTL8111.kext_](https://github.com/Mieze/RTL8111_driver_for_OS_X) - this works with most gigabit Realtek LAN chipsets
* _​_[_RealtekRTL8100.kext_](https://github.com/Mieze/RealtekRTL8100) - for 10/100 Realtek LAN chipsets

### USB

* [_USBInjectAll.kext_ ](https://bitbucket.org/RehabMan/os-x-usb-inject-all/overview)- best explained by the creator of the kext himself:  `In 10.11+ Apple has changed significantly the way the USB drivers work. In the absense of a port injector, the drivers use ACPI to obtain information about which ports are active. Often, this information is wrong. Instead of correcting the DSDT, a port injector can be used (just as Apple did for their own computers)`
* [_GenericUSBXHCI.kext_](https://bitbucket.org/RehabMan/os-x-generic-usb3/overview) _-_ this kext is often needed for USB 3 support, especially on FX. 

### Graphics

* [_WhateverGreen.kext_ ](https://github.com/acidanthera/WhateverGreen)_-_ this kext fixes a lot of GPU related issues.
* [_Lilu.kext_](https://github.com/acidanthera/Lilu) _-_ this kext acts as a loader for other kexts. More specifically it can patch kexts, processes and libraries.

### WiFi and Bluetooth  <a id="wifi-and-bluetooth"></a>

\(I myself don't use Bluetooth nor WiFi so I don't have knowledge in that, but here is some information on the subject by CorpNewt. _Check **Credits** for more info_\)

`Apple is pretty minimal with their WiFi support, so I'll only cover the two main chipsets I'm familiar with. I've used a BCM94360CD + PCIe adapter, and BCM94352HMB/BCM94352Z in my Hackintoshes. The BCM94360CD worked OOB with no extras as it's a native card. For the BCM94352 flavors, I've been using` [`AirportBrcmFixup.kext`](https://github.com/acidanthera/AirportBrcmFixup) `and the companion` [`Lilu.kext`](https://github.com/vit9696/Lilu/releases) `for WiFi setup and` `BrcmBluetoothInjector.kext` `(on 10.13.6+) or` `BrcmPatchRAM2.kext` `alongside` `BrcmFirmwareData.kext` `- all of the Brcm* kexts are from RehabMan's` [`OS-X-BrcmPatchRAM`](https://github.com/RehabMan/OS-X-BrcmPatchRAM) `repo.`

### Audio

* [_VoodooHDA.kext_ ](https://sourceforge.net/projects/voodoohda/)_-_ a jack of all trades master of none solution to audio. Required on FX, but has better alternatives on Ryzen.
* If you are on Ryzen and have a supported codec we will be using native audio, this will be setup later on. This has a better quality than VoodooHDA along with other improvements.

### Misc

* [_NullCPUPowerManagement.kext_](https://github.com/corpnewt/NullCPUPowerManagement) _-_ This kext disables CPU power management, as that is not supported on AMD chips.

### Extra

Depending on what hardware you have in your machine you might need some other kexts. This list is more to be used to give you a general idea, you will probably have to do some google-fu.

