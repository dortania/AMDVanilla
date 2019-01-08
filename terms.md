# Terms

* _Bootloader:_ A piece of software that loads the operating system.
* _Clover:_ This is the bootloader that we will be using. We need this for a few important things. Most importantly:
  * macOS installs on a partition formatted in either APFS or HFS+. A standard \(UEFI\) BIOS cannot read from these formats.
  * It injects kexts on boot.
  * Handles passing information like the SMBIOS to macOS
  * and a lot more.
* _Kext:_ A combination of **K**ernel **Ext**ension. These are additions to the macOS kernel which you can think of like drivers on windows.

