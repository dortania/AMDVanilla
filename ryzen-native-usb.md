---
description: 'Note: This page not yet updated for Mojave.'
---

# Ryzen native USB

### Downloading tools

You will need the following tools to continue:

* [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/)
* Clover Configurator

## DSDT

### Extracting DSDT

Boot your USB drive with clover and press F4. Clover will extract your DSDT to `/EFI/Clover/ACPI/origin`.

### Editing the DSDT

Launch _MaciASL_ and open your previously extracted DSDT with it.

From the topbar go to Preferences, and then Sources.

Click on the + sign to add a new repository and add the following:

```text
Name : Ryzen USB
URL : https://raw.githubusercontent.com/AlGreyy/Ryzen-USB-fix-/master
```

Close this window

Again from the topbar go to Tools and from there Patch. Apply the _USB Ryzen_ patch.

Save the DSDT file from the topbar. \(File, then Save\)

Copy this new DSDT.aml to /EFI/Clover/ACPI/patched.

## Config.plist

Open _Clover Configurator_ and load your config.plist. Go to KextToPatch and add the following things, depending on your OS version:

{% code-tabs %}
{% code-tabs-item title="For 10.13.1 to 10.13.3" %}
```text
Name                       Find                      Replace                Comment
AppleUSBXHCI               21F281FA 000002           21F281FA 000011       ydeng USB patch
AppleUSBXHCI               D1000000 83F901           D1000000 83F910       ydeng USB patch
AppleUSBXHCI               83BD7CFF FFFF0F           83BD7CFF FFFF1F       ydeng USB patch
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="For 10.13.4 to 10.13.6" %}
```text
Name                       Find                      Replace                Comment
AppleUSBXHCI               C8000000 83FB02           C8000000 83FB11       algrey USB patch for ryzen
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now save the config, and reboot your machine. You should now be able to boot in to the macOS installer.

