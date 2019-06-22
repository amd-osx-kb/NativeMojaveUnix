# Kexts

### Where can I find these kexts?

All the kexts shown here are available for download on the [**kext repo**](https://1drv.ms/f/s!AiP7m5LaOED-m-J8-MLJGnOgAqnjGw) provided and maintained by Goldfish64. All these kexts are automagically built when a new kext update is commited.

## What kexts do you need?

### Required
* [VirtualSMC.kext](https://github.com/acidanthera/VirtualSMC) - this kext is required to boot macOS on a regular PC. This kext is what tells macOS "Yes this is a real mac", emulating the functionality of the SMC on real mac's \(from there the name\). Without it, no Hackintosh.
* [FakeSMC.kext](https://github.com/RehabMan/OS-X-FakeSMC-kozlek) - older version of VirtualSMC. VirtualSMC is recommended, since it's more modern. Only use FakeSMC if VirtualSMC doesn't work for you.
* [Lilu.kext](https://github.com/acidanthera/Lilu) _-_ this kext acts as a loader for other kexts. More specifically it can patch kexts, processes and libraries.
* [NullCPUPowerManagement.kext](https://github.com/corpnewt/NullCPUPowerManagement) _-_ This kext disables CPU power management, as that is not supported on AMD chips and can cause kernel panics if enabled.

### Ethernet

* _​_[IntelMausiEthernet.kext](https://github.com/Mieze/IntelMausiEthernet) - this works with most newer Intel LAN chipsets
* _​_[AppleIntelE1000e.kext](https://sourceforge.net/projects/osx86drivers/) - this works with older Intel LAN chipsets - but can cause KPs on newer chipsets
* _​_[AtherosE2200Ethernet.kext](https://github.com/Mieze/AtherosE2200Ethernet) - this works for most Atheros or Killer networking chipsets
* _​_[RealtekRTL8111.kext](https://github.com/Mieze/RTL8111_driver_for_OS_X) - this works with most gigabit Realtek LAN chipsets
* _​_[RealtekRTL8100.kext](https://github.com/Mieze/RealtekRTL8100) - for 10/100 Realtek LAN chipsets

### Graphics

* [WhateverGreen.kext](https://github.com/acidanthera/WhateverGreen)_-_ this kext fixes a lot of GPU related issues.

### WiFi and Bluetooth <a id="wifi-and-bluetooth"></a>

\(I myself don't use bluetooth nor WiFi so I don't have knowledge in that, but here is some information on the subject by CorpNewt. _Check **Credits** for more info_\)  
  
`Apple is pretty minimal with their WiFi support, so I'll only cover the two main chipsets I'm familiar with. I've used a BCM94360CD + PCIe adapter, and BCM94352HMB/BCM94352Z in my Hackintoshes. The BCM94360CD worked OOB with no extras as it's a native card. For the BCM94352 flavors, I've been using` [_`AirportBrcmFixup.kext`_](https://github.com/acidanthera/AirportBrcmFixup) `and the companion` [_`Lilu.kext`_](https://github.com/vit9696/Lilu/releases) `for WiFi setup and` _`BrcmBluetoothInjector.kext`_ `(on 10.13.6+) or` _`BrcmPatchRAM2.kext`_ `alongside` _`BrcmFirmwareData.kext`_ `- all of the Brcm* kexts are from RehabMan's` [_`OS-X-BrcmPatchRAM`_](https://github.com/RehabMan/OS-X-BrcmPatchRAM) `repo.`

### Audio

* [AppleALC.kext](https://github.com/acidanthera/AppleALC) _-_ this kext supports most of the commonly used codecs, with the best quality.

### Extras

Depending on what hardware you have in your machine you might need some other kexts. This list is more to be used to give you a general idea, you will probably have to do some google-fu.

