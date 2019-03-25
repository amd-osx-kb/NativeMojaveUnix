# Windows

## Starting point

I personally prefer to start with an empty config.plist when setting up a desktop, as it means I don't have to worry whether I unticked the correct options. Plus it allows to just have a cleaner config.

I will also be sharing the XML of each section for those who prefer working with a text editor.

## ACPI

### XML

```markup
<key>ACPI</key>
	<dict>
		<key>DSDT</key>
		<dict>
			<key>Fixes</key>
			<dict>
				<key>DeleteUnused</key>
				<true/>
				<key>FixHPET</key>
				<true/>
				<key>FixIPIC</key>
				<true/>
				<key>FixRTC</key>
				<true/>
				<key>FixShutdown</key>
				<true/>
				<key>FixTMR</key>
				<true/>
			</dict>
			<key>Patches</key>
			<array>
				<dict>
					<key>Comment</key>
					<string>change SAT0 to SATA</string>
					<key>Disabled</key>
					<false/>
					<key>Find</key>
					<data>
					U0FUMA==
					</data>
					<key>Replace</key>
					<data>
					U0FUQQ==
					</data>
				</dict>
			</array>
		</dict>
		<key>FixHeaders</key>
		<true/>
	</dict>
```

### Cloud Clover Editor Screenshot

![ACPI page](../../.gitbook/assets/image%20%283%29.png)

### Explanation <a id="explanation"></a>

#### Patches: <a id="patches"></a>

The first thing we'll go over is the _Patches_ section. This section allows us to dynamically rename parts of the DSDT via Clover. Since we're not running a real mac, and macOS is pretty particular with how things are named, we can make non-destructive changes to keep things mac-friendly. We have three entries here:

* _change SAT0 to SATA_ - for potential SATA compatibility

#### Fixes: <a id="fixes"></a>

If we look then at the _Fixes_ section, we'll see that we have a few things checked \(there are 2 pages, so I included 2 screenshots\):

* _FixShutdown_ - this can help with some boards that prefer to restart instead of shutdown. Sometimes it can cause shutdown issues on other boards \(ironic, right?\), so if you have issues shutting down with this enabled, look at disabling it.
* The remaining fixes help avoid IRQ conflicts and etc, and are not known to cause issues. They may not be necessary for all hardware, but do not negatively impact anything if applied.

#### FixHeaders: <a id="fixheaders-and-plugintype"></a>

The only other things we've done on this page are enable that checkbox.

* _FixHeaders_ - This checkbox tells Clover to sanitize headers to avoid kernel panics related to unprintable characters.

## Boot

### XML

```markup
<key>Boot</key>
	<dict>
		<key>Arguments</key>
		<string>-v keepsyms=1 npci=0x3000 debug=0x100</string>
		<key>DefaultVolume</key>
		<string>LastBootedVolume</string>
		<key>Timeout</key>
		<integer>5</integer>
	</dict>
```

### Cloud Clover Editor Screenshot

![Boot](../../.gitbook/assets/image%20%289%29.png)



### Explanation

#### Arguments: <a id="arguments"></a>

We have a few boot args set here:

* `-v` - this enables verbose mode, which shows all the _behind-the-scenes_ text that scrolls by as you're booting instead of the Apple logo and progress bar. It's invaluable to any Hackintosher, as it gives you an inside look at the boot process, and can help you identify issues, problem kexts, etc. _**Remove this for a nice GUI bootscreen when you are done installing.**_
* `debug=0x100` - this prevents a reboot on a kernel panic. That way you can \(hopefully\) glean some useful info and follow the breadcrumbs to get past the issues. 
* `keepsyms=1` - this is a companion setting to `debug=0x100` that tells the OS to also print the symbols on a kernel panic. That can give some more helpful insight as to what's causing the panic itself. _**Keep this only during the install phase as it could cause insecurity in normal use.**_
* `ncpi=0x3000` - this fixes issues with PCI configuration. Without it the machine will often hang on boot.

#### DefaultBootVolume and Timeout: <a id="defaultbootvolume-and-timeout"></a>

These are the only other settings I've updated in this section.

* _DefaultBootVolume_ - this uses NVRAM to remember which volume was last booted by Clover, and auto-select that at the next boot.
* _Timeout_ - this is the number of seconds before the _DefaultBootVolume_ auto-boots. You can set this to `-1` to avoid all timeout, or to `0` to skip the GUI entirely. If set to `0`, you can press any keys at boot to get the GUI to show back up in case of issues.

## CPU

### XML

```markup
<key>CPU</key>
	<dict>
		<key>Latency</key>
		<string>0x3E9</string>
		<key>Type</key>
		<string>0x0604</string>
	</dict>
```

### Cloud Clover Editor Screenshot

![CPU](../../.gitbook/assets/image%20%2815%29.png)

### Explanation

* _Latency/Saving Mode -_ " This parameter value represents the C3 entry latency issued when entering C3 state." or in layman's terms: Disabling speedstep, since AMD CPUs don't support that.
* _Type -_ Determines what CPU name is displayed in _About this mac_

## Devices

### XML

```markup
<key>Devices</key>
	<dict>
		<key>Audio</key>
		<dict>
			<key>ResetHDA</key>
			<true/>
		</dict>
		<key>USB</key>
		<dict>
			<key>FixOwnership</key>
			<true/>
		</dict>
	</dict>
```

### Cloud Clover Editor Screenshot

![Devices](../../.gitbook/assets/image%20%2811%29.png)

### Explanation

#### USB:

Under this section, we ensure that _Inject_ and _FixOwnership_ are selected to avoid issues with hanging at a half-printed line somewhere around the `Enabling Legacy Matching` verbose line. You can also get past that by enabling _XHCI Hand Off_ in BIOS.

#### Audio: <a id="audio"></a>

We enabled _ResetHDA_ which puts the codec back in a neutral state between OS reboots. This prevents some issues with no audio after booting to another OS and then back.

## Disable Drivers

Nothing needs to be done here.

## GUI

### XML

```markup
<key>GUI</key>
	<dict>
		<key>Scan</key>
		<dict>
			<key>Entries</key>
			<true/>
			<key>Linux</key>
			<true/>
			<key>Tool</key>
			<true/>
		</dict>
	</dict>
```

### Cloud Clover Editor Screenshot

![GUI](../../.gitbook/assets/image%20%2831%29.png)

### Explanation

Only a few changes under Scan here. Set it to custom and select _Linux_ and _Tools_. This shows Linux in Clover if you have it installed, and generally cleans up Clover.

## Graphics

If you are on a modern Radeon card you probably need to tick Radeon De-Init, otherewise there's nothing to see here.

## Kernel And Kext Patches

### XML

```markup
<key>KernelAndKextPatches</key>
	<key>KernelAndKextPatches</key>
	<dict>
		<key>AppleRTC</key>
		<false/>
		<key>KernelLapic</key>
		<false/>
		<key>KernelPm</key>
		<false/>
		<key>KextsToPatch</key>
		<array>
			<dict>
				<key>Comment</key>
				<string>External Icons Patch</string>
				<key>Disabled</key>
				<false/>
				<key>Find</key>
				<data>
				RXh0ZXJuYWw=
				</data>
				<key>InfoPlistPatch</key>
				<false/>
				<key>Name</key>
				<string>AppleAHCIPort</string>
				<key>Replace</key>
				<data>
				SW50ZXJuYWw=
				</data>
			</dict>
			g32IDw+DpwQAAA==
		</array>
	</dict>
```

### Cloud Clover Editor Screenshots

![Main page \(for now\)](../../.gitbook/assets/image%20%2839%29.png)

![External Icon Patch](../../.gitbook/assets/image%20%2820%29.png)

![Port Limit Patch](../../.gitbook/assets/image%20%2841%29.png)

### Explanation

The two Kext patches shown on the main screen are added by pressing the + button in the top right of the text window. We have added two patches here. The latter is for USB port limit increases, and the first one acts as an _orange icons fix_ - when internal drives are hotpluggable, and treated as external drives. 

## Rt Variables

### XML

```markup
<key>RtVariables</key>
	<dict>
		<key>BooterConfig</key>
		<string>0x28</string>
		<key>CsrActiveConfig</key>
		<string>0x0</string>
		<key>ROM</key>
		<data>
		O5ycAedp
		</data>
	</dict>
```

### Cloud Clover Editor Screenshot

![Rt](../../.gitbook/assets/image%20%2826%29.png)

### Explanation <a id="explanation-5"></a>

_BooterConfig_ gets set to `0x28`, and _CsrActiveConfig_ is set to `0x3e7` which keeps SIP enabled. You can choose a number of other options to enable/disable sections of SIP. Some common ones are as follows:

* `0x0` - SIP completely enabled
* `0x3` - Allow unsigned kexts and writing to protected fs locations
* `0x3e7` - SIP completely disabled

## SMBIOS

### XML

```markup
<key>SMBIOS</key>
	<dict>
		<key>BiosReleaseDate</key>
		<string>04/09/2018</string>
		<key>BiosVendor</key>
		<string>Apple Inc.</string>
		<key>BiosVersion</key>
		<string>IM142.88Z.0130.B00.1804091831</string>
		<key>Board-ID</key>
		<string>Mac-27ADxxxxxxEE8E61</string>
		<key>BoardManufacturer</key>
		<string>Apple Inc.</string>
		<key>BoardSerialNumber</key>
		<string>D25316xxxxxxxxV1F</string>
		<key>BoardType</key>
		<integer>10</integer>
		<key>BoardVersion</key>
		<string>1.0</string>
		<key>ChassisAssetTag</key>
		<string>iMac-Aluminum</string>
		<key>ChassisManufacturer</key>
		<string>Apple Inc.</string>
		<key>ChassisType</key>
		<string>0x0D</string>
		<key>Family</key>
		<string>iMac</string>
		<key>FirmwareFeatures</key>
		<string>0xE00FE137</string>
		<key>FirmwareFeaturesMask</key>
		<string>0xFF1FFF3F</string>
		<key>LocationInChassis</key>
		<string>Part Component</string>
		<key>Manufacturer</key>
		<string>Apple Inc.</string>
		<key>Mobile</key>
		<false/>
		<key>PlatformFeature</key>
		<string>0x01</string>
		<key>ProductName</key>
		<string>iMac14,2</string>
		<key>SerialNumber</key>
		<string>D25KxxxPFxxC</string>
		<key>SmUUID</key>
		<string>468FxxxF-5xx1-4CD0-BD4E-20xxxxxxE769</string>
		<key>Version</key>
		<string>1.0</string>
	</dict>
```

### Cloud Clover Editor Screenshot

![SMBIOS](../../.gitbook/assets/image%20%286%29.png)

### Explanation

The SMBIOS is what our machine tells macOS it is. In case of a Ryzen based system you want that to be an iMac14,2 as that is about as generic as an SMBIOS gets. _**Do not copy my values, nor use the default values provided in the example plist.**_ Press on the two arrows on the right of the window named `Select a Mac`. Chose the SMBIOS from there.

## System Parameters <a id="system-parameters"></a>

### XML <a id="raw-xml-7"></a>

```markup
<key>SystemParameters</key>
	<dict>
		<key>CustomUUID</key>
		<string>4BxxxxAA-D611-4xx6-978C-0Bxxxxx5F5BD</string>
		<key>InjectKexts</key>
		<string>Yes</string>
		<key>InjectSystemID</key>
		<false/>
		<key>NvidiaWeb</key>
		<true/>
	</dict>
```

### Cloud Clover Editor Screenshot

![System Parameters](../../.gitbook/assets/image%20%2834%29.png)

### Explanation

Inject Kexts is set to 0 so that Clover injects all the kexts we chose before, rather than having to add them to macOS.

## Download

You can now go back to `Cloud Clover Editor`. You can download you config here. Rename the file to config.plist and copy it to _\[your drive\]/EFI/CLOVER/_. Here's my plist, which you can use as an example. Make sure to generate new SMBIOS serials if you plan on using it!

