# macOS

First of all plug in your 8GB drive and make sure there is nothing important on it, _**as it will be wiped**_

Launch Terminal, and run `diskutil list`

This lists all the disks and partitions on the machine. Take note of the device identifier of your USB drive. _**Make sure you have the proper drive as we are about to wipe it**_.

Run the following command, making sure to replace the \# with the identifier of your USB drive:

```bash
diskutil partitionDisk /dev/disk# GPT JHFS+ "USB" 100%
```

This formats your USB drive to a GPT drive with an HFS partition covering 100% of the disk.

Now following [Apple's own guide](https://support.apple.com/en-us/HT201372) you need to run the following command:

```bash
sudo "/Applications/Install macOS Mojave.app/Contents/Resources/createinstallmedia" --volume /Volumes/USB
```

The command above assumes you have the Install macOS.app inside your applications folder, so either place it there, or adjust the command to where you have it stored. Once you run it it will start creating a macOS installer. This takes a good while and doesn't need any input of you, so now is a good time to make some coffee.

Once this is done you will have a USB drive that can boot on a real Intel mac.

Now we need to install Clover on it so that it can boot on a normal PC.

To do so launch the Clover installer you downloaded before and select the USB drive. Now press the `Customise` button.

![Customize button in the bottom left.](../.gitbook/assets/image%20%2827%29.png)

The options that generally are recommended for Ryzen \(and most other hackintoshes\) are shown in the following screenshots.

![UEFI booting only and Install in the ESP](../.gitbook/assets/image%20%288%29.png)

![ApfsDriverLoader and AptioMemoryFix drivers](../.gitbook/assets/image%20%2825%29.png)

![HFSPlus \(You can use VBoxHFS if your copy of the installer doesn&apos;t come with HFSPlus\)](../.gitbook/assets/image%20%281%29.png)



* _Install Clover for UEFI booting only_
* _Install Clover to the ESP_
* _UEFI Drivers:_
  * _AptioMemoryFix_ \(the new hotness that includes NVRAM fixes, as well as better memory management\)
  * _HFSPlus \(or VBoxHfs\)_ - Required for Clover to be able to see HFS+ drives
  * _ApfsDriverLoader_ - \(Available in Dids' Clover builds - or [here](https://github.com/acidanthera/ApfsSupportPkg/releases)\) this allows Clover to see and boot from APFS volumes by loading apfs.efi from ApfsContainer located on block device

**With this setup we can almost boot!**

