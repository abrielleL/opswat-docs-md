<!-- source: https://www.opswat.com/docs/mdendpoint/release-notes/metadefender-endpoint-validation-release-notes -->

# MetaDefender Endpoint Validation Release Notes

| Version | 2611 |
| ---- | ---- |
| **Release date** | November 10, 2026 |
| **Scope/Release Summary** | This release enhanced scan reliability on encrypted media, improved notifications on Windows device; enhanced mobile file-access gating and support custom configuration package support for Linux devices |

### MetaDefender Endpoint Validation - Windows (3.1.2611.1342)

**Release date:** November 10, 2026

Enhancements

- Scan Reliability on Encrypted Media: Fixed an issue where scanning failed on the System Volume Information folder when accessing BitLocker-encrypted USB drives
- Enhanced notification text displaying "Device" and "Downloads" in the popup

Bug fixes

- **Notification Improvements: **Fixed an issue causing overlapping BadUSB and On-Access scan notification popups
- **Validation User Interface & State Handling:** Resolved an issue where the validation progress bar remained stuck in an in-progress state after a USB device was unplugged during validation
- **Security & Packaging: **Fixed an unsigned libcurl.dll in the installer package on Windows Embedded Standard 7

### MetaDefender Endpoint Validation - Linux (3.4.2611.246)

**Release date:** November 10, 2026

Enhancements

- **Enhanced Mobile File-Access Gating: **Enhance mobile file-access protection to cover the rare/direct paths
- **Custom Configuration Package Support:** Administrators can now install and configure MetaDefender Endpoint Validation using tailored configuration packages generated directly by the MetaDefender Endpoint Validation Configuration Tools.

Bug fixes

- **Ubuntu Taskbar Icon: **Fixed an issue on Ubuntu 24.04 and 26.04 where a generic system gear icon appeared on the dock/taskbar instead of the official MetaDefender Endpoint logo.

Known Issues & Limitations

- Admin Password via CLI: Updating the administrator password directly via the CLI command line is currently under triage.
- Window Dragging under Wayland: Moving notification popups may experience positioning constraints under certain Wayland desktop sessions.

> **Supported OS Version**
>
> Ubuntu 20.04
>
> Ubuntu 22.04
>
> Ubuntu 24.04
>
> Ubuntu 26.04

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
