# Acquiring the BaseSystem

Because we need to change the kernel of the installer for one that is compatible with AMD CPUs we can't use the same install process as Intel machines do. Createinstallmedia won't be very useful in this case, and thus we will be getting the BaseSystem.dmg.

## What is the BaseSystem.dmg?

Shortly said, it is what boots when you boot up an installer USB.  
Because of this we need to change its kernel with the AMD one as well to be able to boot it. It does not hold the installer for the OS in it though.

## Where do I get this mystical BaseSystem.dmg?

First you will need a copy of macOS 10.13.6. That's the latest version of High Sierra and with that the OS this guide was written for. _**You need the full multiple gigabyte installer, not the 16 MB stump.**_ _Now how do I get this image?_ The .dmg is very easy to acquire, and it is done as follows:

1. Navigate to the directory of your _"Install macOS High Sierra.app"_ file.
2. Right click on the file and press _"Show package contents"_
3. Go to _"/Contents/Shared Support/"_
4. BaseSystem will be right there, copy it to a easily memorable location. \(The desktop is what I will be using later on in the guide.\)

