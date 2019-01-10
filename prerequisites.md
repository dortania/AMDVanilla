# Prerequisites

This guide focuses on desktops as integrated AMD graphics sadly do not work in macOS. This means that laptop will not have any acceleration \(same goes for APUs, unless you add a separate GPU\).  
So far this guide has only been tested on Ryzen CPUs.

What will you need to make an installer:

* an 8GB or larger USB drive
* Install macOS Mojave.app \(10.14.1, preferably from the [App Store](https://itunes.apple.com/us/app/macos-mojave/id1398502828?mt=12)\)
* [Clover installer](https://github.com/Dids/clover-builder/releases) \(Daily builds done courtesy of Dids\)
* [Clover Configurator ](http://mackie100projects.altervista.org/download-clover-configurator/)\(You can also use any text editor, but CC is generally a lot faster\)
* ~~~~[~~FakeSMC.kext~~](https://bitbucket.org/RehabMan/os-x-fakesmc-kozlek/downloads/) ~~\(The one kext you absolutely need. It emulates the SMC of a Mac and basically tells macOS "Yes this is a real mac, you are free to boot"\)~~
  * These days a modern alternative to the FakeSMC.kext has emerged:
  * [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC) It does the same basic things as FakeSMC but is the more modern and recommended alternative. Use FakeSMC only if VirtualSMC does not work.
  * [Installer kexts](https://github.com/Shaneee92/Mojave_AMD_XNU/releases) \(These are first party Apple kexts that are needed to rebuild the kextcache, but are missing from the installer. These specific ones are for 10.14.1.\)
* [The AMD kernel ](https://github.com/Shaneee92/Mojave_AMD_XNU/releases)\(Extract the .zip to your desktop, futher commands using it will be based on it being on the desktop\)
* Any kexts that are needed for your specific hardware
* A cup of coffee \(or a few\)
* Patience
* Some good Google-fu

