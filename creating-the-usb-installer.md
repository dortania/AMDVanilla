# Creating the USB installer

Before we can start with making the actual installer we will need to prepare the 8+ GB USB drive. You need to make sure your drive is set up in the following way:

* GUID Partition Map \(GPT\)
* 1 Data partition
* OSX Extended \(Journaled\) \(jHFS+\)

We are going to execute some commands in the terminal to achieve this. To open the terminal you need to do the following:

1. Open Finder
2. go to _Applications_
3. go to _Utilities_
4. double click on _Terminal_

Now that you have Terminal open run `diskutil list`, this command will list all the drives connected to your machine and their partitions. Note down the identifier for your USB drive, this will be needed later.

_**DO NOT GUESS, WE ARE ABOUT TO ERASE THAT DRIVE.**_

Run the following command with `disk#` replaced by your identifier.

```bash
diskutil partitionDisk /dev/disk# GPT JHFS+ "USB" 100%
```

* `diskutil`- This is the program we are executing, short for Disk Utility
* `partitionDisk`- Pretty selfexplanatory, tells diskutil that we are want to partition a disk.
* `/dev/disk#`- The drive we want to edit.
* `GPT`- Use GUID partition map.
* `JHFS+ "USB" 100%`- Make a partition called _USB_ using the entirety of the disk and format it as JHFS+.

The following command assumes you have your BaseSystem.dmg on your desktop. Adjust if needed.

_**Replace the \# with your disk's identifier**_

```bash
sudo asr restore -source ~/Desktop/BaseSystem.dmg -target /dev/disk#s2 --erase
```

_This takes a lot of time and doesn't create a lot of output_. It can take a good 30-40 minutes on a weaker machine, so just because it doesn't change anything on screen don't assume it froze. Grab a cup of good coffee, talk with your family, watch an episode of your favourite show and come back after that, it should be done.

Once that's done, drag the `Install macOS Mojave.app` that you have onto your USB. This will copy the entire installer and not use network recovery, as the latest version of Mojave \(which network recovery will install\) does not have an AMD kernel yet.

When this is all done you will have a USB drive that can boot the full macOS installer on a real Mac. You only need to add a few hackintosh specific things and you will be ready to go.

At some point in the future I might write a script that does this for you. For the lazy and/or easily scared by the command line.

