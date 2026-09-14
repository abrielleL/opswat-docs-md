<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/does-oesis-support-microsoft-hotpatch-for-patch-management -->

# Does OESIS support Microsoft Hotpatch for patch management?

## [Overview](/docs/mdsdk/knowledge-base/does-oesis-support-microsoft-hotpatch-for-patch-management#overview)

Microsoft Hotpatch introduces a new patching mechanism that allows certain security updates to be applied to a running system without requiring a reboot. This capability is primarily available on Windows Server Azure Edition and relies on hotpatch-enabled binaries and in-memory code updates.

At this time, OESIS does not support Microsoft Hotpatch. OESIS’s patch detection and management capabilities are designed around the traditional Windows patching model, where updates are installed through standard Windows Update mechanisms and applied at the system level, often requiring a reboot.

Because Microsoft Hotpatch follows a different technical approach from traditional patching, including how updates are applied and how patch state is represented, the updates applied via Hotpatch are not currently supported by OESIS.

## [What OESIS supports today](/docs/mdsdk/knowledge-base/does-oesis-support-microsoft-hotpatch-for-patch-management#what-oesis-supports-today)

OESIS:

- Detects and manages patches installed via **traditional Windows Update**
- Relies on **standard KB installation records** and operating system–level patch metadata
- Supports environments that follow Microsoft’s **conventional patch lifecycle** (exclude C/D release)

## [Impact for environments using Microsoft Hotpatch](/docs/mdsdk/knowledge-base/does-oesis-support-microsoft-hotpatch-for-patch-management#impact-for-environments-using-microsoft-hotpatch)

When Microsoft Hotpatch is enabled:

- Hotpatched updates may **not be detected or managed** by OESIS
- Patch status reported by OESIS may **not fully reflect** updates applied via Hotpatch
- OESIS continues to report accurately for **non-Hotpatch (traditional) updates**

## [Future considerations](/docs/mdsdk/knowledge-base/does-oesis-support-microsoft-hotpatch-for-patch-management#future-considerations)

Microsoft Hotpatch represents a new direction in Windows patching, and support for it would require dedicated technical changes. While OESIS does not currently support Hotpatch, this is an area we continue to monitor as Microsoft evolves the technology and adoption increases.
