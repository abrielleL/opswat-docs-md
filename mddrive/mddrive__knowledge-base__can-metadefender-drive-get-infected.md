<!-- source: https://www.opswat.com/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected -->

# Can MetaDefender Drive get infected with viruses?

**Check Your Version:**

This article applies to all MetaDefender Drive releases deployed on Windows and Linux systems.

## [**Overview**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#overview)

MetaDefender Drive is designed to scan potentially compromised systems from a trusted bootable USB environment. In normal **Pre-Boot Scan** usage, the target computer is powered off, MetaDefender Drive is inserted, and the system is booted from the MetaDefender Drive USB device. In this mode, the operating system installed on the target computer is not running, which significantly reduces the risk that malware from that installed operating system can interact with or modify MetaDefender Drive during the scan.

However, MetaDefender Drive should not be understood as a completely read-only USB device. It includes writable areas required for normal operation, including logs, update data, support information, configuration data, and engine packages. For example, MetaDefender Drive logs are stored under the `/persistence` area, and engine updates can be copied to the Drive using MetaDefender Drive Toolkit.

Because MetaDefender Drive contains writable storage areas, a running host operating system may be able to write files to the visible writable partitions when the Drive is inserted into that system. This is a general removable-media behavior and is not unique to MetaDefender Drive.

## [**Is MetaDefender Drive read-only?**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#is-metadefender-drive-read-only)

No. MetaDefender Drive is not fully read-only.

Some areas of the Drive must remain writable so that MetaDefender Drive can perform supported operations such as storing logs, saving support data, applying updates, copying engine packages, and maintaining product state. The existence of writable areas does not mean the Drive is unprotected, but it does mean it should not be treated as a physically write-protected USB device.

MetaDefender Drive Toolkit also supports reflashing or reinstalling the MetaDefender Drive software image onto supported drives. This process is used to upgrade or reinstall the Drive software and prepare the device to boot using the newly flashed software.

## [**What happens during a Pre-Boot Scan?**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#what-happens-during-a-pre-boot-scan)

During a Pre-Boot Scan, the target system is started from MetaDefender Drive instead of the operating system installed on the internal disk. Our documentation recommends inserting MetaDefender Drive while the target device is turned off, powering the device on, and then booting from MetaDefender Drive.

In this scenario, typical malware that depends on the installed operating system being active is not running. As a result, it generally cannot behave as it would during a normal Windows, Linux, or macOS session, and it cannot normally copy itself to removable media through the installed operating system during the scan.

This is one of the reasons Pre-Boot Scan is the preferred approach when scanning systems that may already be compromised.

## [**What happens if MetaDefender Drive is inserted into a running operating system?**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#what-happens-if-metadefender-drive-is-inserted-into-a-running-operating-system)

The risk model is different when MetaDefender Drive is inserted into a computer while that computer’s operating system is already running.

In that case, the host operating system can see the writable areas of the Drive that are exposed for supported workflows. If the host operating system is compromised, malware on that system may attempt to write files to removable media, including MetaDefender Drive.

This does not necessarily mean that the MetaDefender Drive boot environment itself has been compromised. A malicious or suspicious file may be written to a writable partition without replacing or modifying the trusted MetaDefender Drive software environment.

## [**Built-in protection behavior**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#built-in-protection-behavior)

MetaDefender Drive includes protection behavior intended to preserve the integrity of the Drive environment.

When MetaDefender Drive boots into its secure environment, it audits its own filesystem. The Drive is designed to allow only expected OPSWAT components, logs, configuration files, and required directories to remain. If unauthorized files are present on the MetaDefender Drive partition, they are automatically removed. If configuration scripts are altered, MetaDefender Drive refuses to boot.

When the Drive is connected to a running host and managed through MetaDefender Drive Toolkit, the Toolkit also validates that the device is an authorized MetaDefender Drive hardware unit and audits the filesystem for unauthorized files written by the host OS.

This protection behavior means that a file being copied to a writable area of the USB device is not the same as the MetaDefender Drive operating environment being persistently infected.

## [**Can MetaDefender Drive become infected?**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#can-metadefender-drive-become-infected)

In normal Pre-Boot Scan usage, the risk of the target system infecting MetaDefender Drive is low because the target system’s installed operating system is not running during the scan.

MetaDefender Drive is not fully read-only, so writable areas of the Drive can be modified when the Drive is connected to a running host operating system. A compromised host operating system may attempt to write unwanted or malicious files to removable media. MetaDefender Drive includes protection and validation mechanisms designed to remove unauthorized files and preserve the integrity of the Drive environment.

Therefore, the most accurate answer is:

**MetaDefender Drive is not a fully read-only device, but it includes protection mechanisms that help prevent unauthorized files from remaining on the Drive and help protect the integrity of the MetaDefender Drive environment. In standard Pre-Boot Scan usage, typical malware from the target operating system is not active during the scan and generally cannot infect the Drive in the normal removable-media propagation sense.**

## [**When should MetaDefender Drive be reflashed?**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#when-should-metadefender-drive-be-reflashed)

If the integrity of a MetaDefender Drive device is in doubt, the recommended remediation is to reflash or reinstall the MetaDefender Drive software using MetaDefender Drive Toolkit.

MetaDefender Drive Toolkit can upgrade or reinstall the MetaDefender Drive software by flashing the downloaded software image. Once the flashing process completes successfully, the Drive is ready to boot using the newly flashed software.

## [**Best practices**](/docs/mddrive/knowledge-base/can-metadefender-drive-get-infected#best-practices)

For the highest level of protection, use MetaDefender Drive in Pre-Boot Scan mode when scanning systems suspected of compromise. Insert the Drive while the target system is powered off, boot directly from MetaDefender Drive, and perform the scan from the MetaDefender Drive environment.

When updates, logs, or support data must be handled, use a trusted management workstation and MetaDefender Drive Toolkit whenever possible. Avoid unnecessary interaction with the writable partitions of MetaDefender Drive from systems suspected to be compromised.

If there is any concern that the Drive was modified while connected to an untrusted or infected system, reflash the Drive using MetaDefender Drive Toolkit before using it again in a trusted workflow.

**Support:**

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
