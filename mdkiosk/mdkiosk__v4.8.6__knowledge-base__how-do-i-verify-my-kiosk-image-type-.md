<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-verify-my-kiosk-image-type- -->

# How do I verify my Kiosk Image type?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MD Kiosk versions

MetaDefender Kiosk supports multiple deployment types on Windows. The following instructions will help you verify whether your system is using the Kiosk Hardened Image, Secure Image, or the standalone Kiosk Software.

1. Via the support package.

When exporting the Kiosk support package, a file named `imageType.info` is included. You can open this file using Notepad to view the deployment type.

**Software Edition**: The user installed the Kiosk software manually.

**Hardened Image**: The OS was flashed with a Hardened Image.

**Secure Image**: The OS was flashed with Secure Image

Info:

The method above only applies to MD Kiosk 4.7.1 or above

2. Via registry.

You can browse this registry to check the Kiosk information HKLM\SOFTWARE\WOW6432Node\OPSWAT\MD4M

“harden_image” = 0 means The user installed the Kiosk software manually.

“harden_image” = 1 means The OS was flashed with a Hardened Image.

“secure_image” = 1 means The OS was flashed with Secure Image.

TIPS:

- Customers who purchase Kiosk Hardware will receive the Kiosk Hardened Image pre-installed as the operating system.
- **Secure Image** is a specialized version of the Hardened Image, enhanced with a File Integrity Monitoring feature. This edition requires an additional license and is available for selected Kiosk hardware or upon request.
Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
