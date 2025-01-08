# Surface-Laptop-Go-OpenCore
 macOS on the Microsoft Surface Laptop Go thanks to Acidanthera's OpenCore bootloader.

## Software Specifications
| Software         | Version                            |
| ---------------- | ---------------------------------- |
| Target OS        | Apple macOS 13 Ventura, 14 Sonoma and 15 Sequoia |
| OpenCore         | [MOD-OC v1.0.3](https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases/download/1.0.3_20b758b/OpenCore-Mod-1.0.3-RELEASE.zip) |
| SMBIOS           | MacBookAir9,1 |
| SSD format       | APFS file system, GPT partition table |

## Abstract
Everything on the Core 1035G1 Surface Laptop Go is working perfectly like on a real Mac.

The Surface Laptop Go works great as a handy little macOS laptop.

The battery runtime is around five hours.

> [!TIP]
> I recommend installing `macOS 13 Ventura` rather than the newer `macOS 14 Sonoma` or `macOS 15 Sequoia`. The builtin Intel Wireless chip works almost perfectly with Apple's iServices and Continuity features on Ventura while those features are partially broken at the moment on newer versions of macOS.

> [!IMPORTANT]
> For macOS to be able to boot on the Surface Laptop Go, the `Secure Boot` option _**must be disabled**_ in the UEFI. The boot screen will then display a large red bar with a padlock symbol at the top of the display when Secure Boot is disabled.

## Disclaimer
This repository is neither a howto nor an installation manual. Using these files requires at least basic knowledge of [Acidanthera's OpenCore bootloader](https://github.com/acidanthera/OpenCorePkg), ACPI, UEFI and the art of hackintoshing in general. I recommend reading the excellent [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide), as well as all its linked resources. For those who wish to improve their hackintoshing knowledge, [5T33Z0's OC-Little-Translated](https://github.com/5T33Z0/OC-Little-Translated) repository is the most comprehensive resource I've found on the subject.

## Recommendations
I recommend completely erasing the device's SSD by creating a new GPT partition table before attempting to install macOS, as it makes the installation process much easier. You may use any Linux live ISO with a partitioning tool such as `GParted` or `KPartition` to erase the SSD.

Please be aware that all `PlatformInfo` and `SMBIOS` information was removed from the OpenCore `config.plist` files. Users will therefore need to generate their own `PlatformInfo` with [CorpNewt's GenSMBIOS tool](https://github.com/corpnewt/GenSMBIOS) before attempting to boot a Surface Go 2 with this repository's EFI folder.

`AirportItlwm-Ventura.kext`, `AirportItlwm-Sonoma140.kext` and `AirportItlwm-Sonoma144.kext` from the [OpenIntelWireless repo](https://github.com/OpenIntelWireless/itlwm) are required to enable the Wifi chip. This EFI will dynamically load the appropriate kext for macOS Ventura or Sonoma depending on the running kernel. No need to manually replace the kext file when updating your version of macOS. As the Intel Wifi chip does not yet work with the `AirportItlwm.kext` in macOS Sequoia, you'll need to use the `Itlwm.kext` and its companion app [HeliPort](https://github.com/OpenIntelWireless/HeliPort/releases) to connect to a Wifi network. You'll find the latest stable `HeliPort.dmg` in the [Tools folder](https://github.com/jlempen/Surface-Laptop-Go-OpenCore/blob/main/Tools/HeliPort.dmg) of this repo. This EFI will dynamically load the `Itlwm.kext` instead of `AirportItlwm.kext` when you boot into macOS Sequoia.

Windows and Linux should be detected automagically by the OpenCore boot loader even when installed after macOS.

This repository uses the unofficial OpenCore_NO_ACPI_Build fork of OpenCore by [btwise](https://gitee.com/btwise/OpenCore_NO_ACPI), wich is not endorsed by Acidanthera (the dev team behind OpenCore). The main (and only) difference between this fork and the official OpenCore version is that it allows to prevent ACPI injection (e.g. patches, tables, boot parameters) into other OSes besides macOS.
