# Windows

Plug in your USB drive.

Download and extract gibMacOS from CorpNewt's repo as linked in Prerequisites.

Double click on gibMacOS.bat. This will run gibMacOS, and if needed install Python while it's at it.

![GibMacOS.bat](../.gitbook/assets/image%20%2817%29.png)

Now type `r` and press enter to enable recovery only mode.

![](../.gitbook/assets/image%20%2812%29.png)

Now type `1` and press enter to select the latest version.

![](../.gitbook/assets/image%20%2837%29.png)

After you do this GibMacOS will start to download the file. This takes a while depending on your connection. When it is done, quit the tool. Now run MakeInstall.bat. A UAC prompt will show, which you have to accept, and then the tool will download it's requirements. When it is done you will be greeted by the following screen:

![](../.gitbook/assets/image%20%2835%29.png)

Now **MAKE SURE YOU HAVE THE PROPER DRIVE** as we will be erasing it. Type in the number of your drive and then press enter. In my case I need `3`. Now you need to give the tool some time again as it sets up the USB drive and installs Clover to it. The following screen will show when it's done:

![](../.gitbook/assets/image%20%2827%29.png)

Browse to `GibMacOS` &gt; `macOS Downloads` &gt; `publicrelease` &gt; _`[macOS version]`._ Hold down shift and right click on the file. Press `Copy as Path`. Right click again in the cmd window to paste the path. Now press enter and it will start extracting.

![](../.gitbook/assets/image%20%2816%29.png)

The extraction process takes quite a while, so don't be discouraged if it sticks on the following screen for a long time:

![](../.gitbook/assets/image%20%2810%29.png)

The following message will appear once it's done:

![](../.gitbook/assets/image%20%2821%29.png)

Browse to _\[Your drive\]/EFI/Clover_ and delete the config.plist that is there. We'll be adding our own later on. Now go to the _drivers64UEFI_ folder and delete everything that is inside it. Go to Drivers-off/drivers64UEFI and copy the following files to /EFI/Clover/drivers64UEFI:

![Required drivers](../.gitbook/assets/image.png)

Now paste all your kexts in to /EFI/Clover/kexts/Other. FakeSMC.kext should already be there. You can use it, or replace it with VirtualSMC if you so desire. Remember to add the unzipped .kext folders, not the .zip files you get from the repo. Here's an example of what it should look like:

![](../.gitbook/assets/image%20%2818%29.png)

At this point all we have left to do is set up a config, which you can read about in the following chapter.

