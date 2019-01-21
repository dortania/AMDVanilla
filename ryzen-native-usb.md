# Ryzen native USB

### Downloading tools

You will need the following tools to continue:

* [MaciASL](https://bitbucket.org/RehabMan/os-x-maciasl-patchmatic/downloads/)
* Clover Configurator

## DSDT

### Extracting DSDT

Boot your USB drive with Clover and press F4. Clover will extract your DSDT to `/EFI/Clover/ACPI/origin`.

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

Open _Clover Configurator_ and load your config.plist. Go to KextToPatch and add the following things:

{% code-tabs %}
{% code-tabs-item title="For 10.14.1" %}
```text
Name                       Find                      Replace                Comment
AppleUSBXHCI               C7000000 4183FD02         C7000000 4183FD11      algrey USB patch for ryzen
AppleUSBXHCI               83FB0F0F 838F0400 00      83FB0F90 90909090 90   disable port limit in XHCI kext (credit DalianSky,Ricky)
```
{% endcode-tabs-item %}
{% endcode-tabs %}

Now save the config, and reboot your machine. You should now be able to boot in to the macOS installer.

