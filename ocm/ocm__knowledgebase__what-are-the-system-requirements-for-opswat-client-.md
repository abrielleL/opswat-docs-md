<!-- source: https://www.opswat.com/docs/ocm/knowledgebase/what-are-the-system-requirements-for-opswat-client- -->

# What are the system requirements for MetaDefender Endpoint?

This article applies to all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, iOS and Android systems.

To meet the needs of customers managing a range of unique devices, MetaDefender Endpoint supports the majority of leading operating systems, including:

- Windows
- macOS
- iOS
- Android
- Ubuntu
- Centos
- Mint
- Redhat Enterprise
- Open Suse
- Suse Enterprise
- Open Source IoT (Internet of Things)

Pro Tip:

The MetaDefender Endpoint is a lightweight, unobtrusive application, designed to run on every device that is being managed by your account on either OPSWAT Central Management or MetaAccess.

As such, system requirements per device are minimal.

## [To install MetaDefender Endpoint on a device, that device must meet the following minimum system requirements:](/docs/ocm/knowledgebase/what-are-the-system-requirements-for-opswat-client-#to-install-metadefender-endpoint-on-a-device-that-device-must-meet-the-following-minimum-system-requirements)

| Operating System Family | Minimum OS Version | Minimum system requirements |
| --- | --- | --- |
| **Windows**(1) | Windows 7  Windows Server 2008 | CPU: 1 GHz Hard disk space: 500MB |
| **macOS** | OSX 10.9 | CPU: 1 GHz Hard disk space: 500MB |
| **Linux v3** (14.4.x.y) | CentOS 7  Ubuntu 14.4 | CPU: 1 GHz Hard disk space: 500MB |
| **Debian-based Linux v4** (15.4.x.y) | Ubuntu 16+  Mint 18+  Debian 8+ | CPU: 1 GHz Hard disk space: 500MB |
| **Red hat-based Linux v4** (15.6.x.y) | CentOS 7.14+ Redhat Enterprise 7+  OpenSuse 11.4+ Suse Enterprise 12x +  Fedora 27+ | CPU: 1 GHz Hard disk space: 500MB |
| **iOS** | iOS 8.3+ | iPhone 5s iPad (4th generation) iPad Air iPad mini |
| **Android** | Android 5.1+ | Memory: 1.5GB |

Please Note:

For security reasons, all devices must support TLS 1.2 (Transport Layer Security 1.2) or above.

If your Windows system is not yet configured to support TLS 1.2 or above, please follow the guidelines, [Here](https://support.microsoft.com/en-us/topic/update-to-enable-tls-1-1-and-tls-1-2-as-default-secure-protocols-in-winhttp-in-windows-c4bd73d2-31d7-761e-0178-11268bb10392).

MacOS and Linux users should research TLS enablement options via their either Apple or Linux documentation though, in the case of Linux, enablement is a fairly standard command line process. In addition, users can consult the guidelines [Here](https://support.apple.com/guide/security/tls-security-sec100a75d12/web) (for macOS), and [Here](https://www.adminbyaccident.com/security/how-to-configure-tls-1-2-on-unix-or-gnu-linux/) (for Linux).

### [(1)Additional requirements for legacy Windows systems include:](/docs/ocm/knowledgebase/what-are-the-system-requirements-for-opswat-client-#1additional-requirements-for-legacy-windows-systems-include)

In order to run the MetaDefender Endpoint, legacy Windows devices must have the following KBs installed.

- Windows 7 and Windows Server 2008:

  - **KB2533623** - please [Read This](https://support.microsoft.com/en-us/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704)
  - **KB3033929 -** please [Read This](https://support.microsoft.com/en-us/topic/microsoft-security-advisory-availability-of-sha-2-code-signing-support-for-windows-7-and-windows-server-2008-r2-march-10-2015-d1b1b28c-b7fa-2902-f5a2-dc533812df7a)
- Windows Server Small Business Server Standard FE (version 2011 Standard):

  - **KB2533623** - please [Read This](https://support.microsoft.com/en-us/topic/microsoft-security-advisory-insecure-library-loading-could-allow-remote-code-execution-486ea436-2d47-27e5-6cb9-26ab7230c704).

Support:

For queries, concerns or issues meeting **The Minimum Device Requirements For** MetaDefender Endpoint, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
