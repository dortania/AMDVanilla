---
description: A quick and dirty guide on making a vanilla AMD hackintosh.
---

# Vanilla AMD Hackintosh

## Why vanilla?

### It's clean

The AMD distros are designed to be ran on various different hardware combinations, while a vanilla install is made for your specific hardware. This means that your install will only have what it needs and no extra useless junk.

### Tailor made for your hardware

A vanilla install doesn't have any unneeded kexts or modifications which could cause issues.

### More instructive

Making your own install teaches you a lot more about how hackintoshing works which in turn makes it easier for you to troubleshoot any potential issues.

## The good, the bad and the ugly:

### What works

* AMD Ryzen CPUs
* Native USB
* Native Audio
* The latest version of macOS High Sierra
* iCloud
* AMD GPUs

So much works, that it is easier to say what doesn't so here we go:

* AMD FX CPUs \(I don't have one to use for testing\)
* Internal Graphics. Be it an AMD Ax CPU or one of the G Ryzen chips, the GPU will **not** work.
* Nvidia GPUs requiring Nvidia Web Drivers \(no Web Drivers yet\)
* Lower GPU performance, more specifically:
  * About 10% lower on AMD GPUs
  * About 75% lower on Nvidia GPUs
* IOMMU
* iMessage, FaceTime
* Siri

