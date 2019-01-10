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
* Native Audio
* macOS Mojave 10.14.1
* iCloud
* AMD GPUs
* Nvidia GPUs not requiring Nvidia Web Drivers

So much works, that it is easier to say what doesn't so here we go:

* AMD FX CPUs \(I don't have one to use for testing\)
* Any other version of Mojave \(Kernel sources haven't been released for other versions, so no patched AMD kernels\)
* Internal Graphics. Be it an AMD Ax CPU or one of the G Ryzen chips, the GPU will **not** work.
* Nvidia GPUs requiring Nvidia Web Drivers \(no Web Drivers yet\)
* Lower GPU performance, more specifically:
  * About 10% lower on AMD GPUs
  * ~~About 75% lower on Nvidia GPUs~~
    * I have been told that this is not the case. Performance varies a lot per model, but it is safe to assume it is a lot lower than on Windows.
* IOMMU
* iMessage, FaceTime
* Siri

