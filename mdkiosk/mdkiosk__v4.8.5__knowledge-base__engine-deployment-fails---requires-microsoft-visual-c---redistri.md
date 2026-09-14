<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/engine-deployment-fails---requires-microsoft-visual-c---redistri -->

# Engine deployment fails: "requires Microsoft Visual C++ Redistributable 14.44 or higher" (issue resolved)

## [Symptoms](/docs/mdkiosk/v4.8.5/knowledge-base/engine-deployment-fails---requires-microsoft-visual-c---redistri#symptoms)

The issue has been resolved!

This issue has since been resolved on the engine side. If you encounter the error, simply re-trigger the engine update.

The new version of engines no longer requires VC++ Redistributable 14.44. Instead, it works with version 14.38, which is bundled in Kiosk Hardened Image 26.05 or older).

If you have already installed 14.44, everything will continue to work without any issues.

On the Kiosk Hardened Image (version 26.05 or older), some engines may have failed to deploy when Core downloaded or updated them. The affected engines are File Type, Archive Compression, Archive Extraction, CDR, and Country of Origin. The deployment error stated that Microsoft Visual C++ Redistributable must be upgraded to version 14.44 or higher.

One or more of the following engines fail to deploy during download or update

- File Type
- Archive Compression
- Archive Extraction
- CDR
- Country of Origin

Error message: *"Requires Microsoft Visual C++ Redistributable version 14.44 or higher."*

## [Cause](/docs/mdkiosk/v4.8.5/knowledge-base/engine-deployment-fails---requires-microsoft-visual-c---redistri#cause)

The previously released engine versions required Microsoft Visual C++ Redistributable version 14.44 or higher. On the Kiosk Hardened Image (26.05 or older), the installed Microsoft Visual C++ 2015–2022 Redistributable is version 14.40 (or older), which did not meet that requirement — so the deployment failed.

**This engine change has since been reverted, so the engines no longer require version 14.44.**

## [Resolution](/docs/mdkiosk/v4.8.5/knowledge-base/engine-deployment-fails---requires-microsoft-visual-c---redistri#resolution)

The engine change has been reverted, so this issue should no longer occur.

If you still encounter the error, simply re-trigger the engine download/update in Core:

1. Re-run the engine download/update in Core.
2. Confirm the previously failing engines now deploy successfully.

### [Optional Approach](/docs/mdkiosk/v4.8.5/knowledge-base/engine-deployment-fails---requires-microsoft-visual-c---redistri#optional-approach)

Although it is no longer required, you may still upgrade the Microsoft Visual C++ Redistributable to version 14.44 or higher:

- **x64:** <https://aka.ms/vs/17/release/vc_redist.x64.exe>
- Reference page (all architectures and current version): <https://learn.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist>

Microsoft Visual C++ Redistributable 14.51 (2015–2022) in Kiosk Hardened Image 26.06

Kiosk Hardened Image 26.06 will ship with Microsoft Visual C++ Redistributable 14.51 (2015–2022).
