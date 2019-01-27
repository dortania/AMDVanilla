# Acquiring the BaseSystem

Because we need to change the kernel of the installer for one that is compatible with AMD CPUs we can't use the same install process as Intel machines do. `createinstallmedia` won't be very useful in this case, and thus we will be getting the BaseSystem.dmg.

## What is the BaseSystem.dmg?

Shortly said, it is what boots when you boot up an installer USB.  
Because of this we need to change its kernel with the AMD one as well to be able to boot it. It does not hold the installer for the OS in it though.

## Where do I get this mystical BaseSystem.dmg?

First you will need a copy of macOS 10.14.1. That's the only version of Mojave with an AMD kernel released and that this guide was written for. _**You need the full multiple gigabyte installer, not the 16 MB stump.**_ _Now how do I get this image?_ The .dmg is very easy to acquire, and it is done as follows:

1. Navigate to the directory of your _"Install macOS Mojave.app"_ file.
2. Right click on the file and press _"Show Package Contents"_
3. Go to _"/Contents/SharedSupport/"_
4. BaseSystem.dmg will be right there, copy it to a easily memorable location. \(The desktop is what I will be using later on in the guide.\)

