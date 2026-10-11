<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/why-is-paragon-software-disappeared-after-i-installed-an-older-v -->

# Why is Paragon software disappeared after I installed an older version of Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Issue:](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-paragon-software-disappeared-after-i-installed-an-older-v#issue)

- After reinstalling an older version of Kiosk (4.7.5 or earlier), the Kiosk fails to detect Linux file systems. Upon inspection, the Paragon software is missing from the Kiosk machine.

### [Possible cause:](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-paragon-software-disappeared-after-i-installed-an-older-v#possible-cause)

- Kiosk relies on the Paragon software to detect Linux file systems. If Paragon is missing, detection will fail. Starting with Kiosk 4.7.6, the bundled Paragon software was upgraded to version 6.1.289. When Kiosk is uninstalled, this version remains on the device (by design).
- If an older version of Kiosk (4.7.5 or earlier) is reinstalled, it attempts to install its older Paragon version over the existing one. This version conflict can result in Paragon being completely removed.

### [**Solution**:](/docs/mdkiosk/v4.8.6/knowledge-base/why-is-paragon-software-disappeared-after-i-installed-an-older-v#solution)

- **Approach 1**: Open the Kiosk installer → Select Repair → Restart the system. Paragon will be reinstalled successfully.
- **Approach 2**: Uninstall the current (older) Kiosk version → Reinstall the same version → Paragon will be reinstalled successfully.
