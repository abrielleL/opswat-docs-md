<!-- source: https://www.opswat.com/docs/mddrive/v4.4.8/knowledge-base/secureboot-known-issues -->

# SecureBoot Known Issues

#### [Overview](/docs/mddrive/v4.4.8/knowledge-base/secureboot-known-issues#overview)

MetaDefender Drive is designed to boot on a wide range of UEFI‑based systems with Secure Boot enabled. On the majority of devices (laptops, desktops and workstations from major vendors such as Dell, HP, Lenovo, Siemens, etc.), the device recognizes MetaDefender Drive as a valid EFI boot option and starts it without any additional configuration.

#### [Manual Selection If Necessary](/docs/mddrive/v4.4.8/knowledge-base/secureboot-known-issues#manual-selection-if-necessary)

Some vendor implements Secure Boot, key management, and boot menus differently, a small subset of systems may require manual boot selection or specific firmware settings. On those UEFI systems, the firmware does not automatically prioritize the default boot loader used on MetaDefender Drive (for example, the “Grub X64 (OPSWAT MetaDefender)” entry). In those cases:

- The USB device may not appear as a normal boot option, **or**
- Selecting the “Grub X64 (OPSWAT MetaDefender)” entry may result in a boot failure, even though Secure Boot is enabled and working for other devices.

However, the same firmware typically still allows the user to:

- Use **“Boot from File”** (or a similar menu entry) in the BIOS/UEFI setup, then
- Manually browse to the MetaDefender Drive USB and select the EFI binary directly (usually `BOOTX64.EFI`).

Once the correct file is selected and booted at least once, many systems will remember this boot entry and boot MetaDefender Drive normally in subsequent sessions.

#### [Known Issues](/docs/mddrive/v4.4.8/knowledge-base/secureboot-known-issues#known-issues)

There is a known issue with Surface devices, where Microsoft utilizes proprietary UEFI/BIOS locks on Surface devices that often obstruct Linux boot loaders, requiring complex workarounds like disabling Secure Boot.

There are no other known issues at this time.
