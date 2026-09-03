<!-- source: https://www.opswat.com/docs/ocm/troubleshooting/ochelper-unc -->

# OCHelper.exe reported the error "Attempting to perform the InitializeDefaultDrives operation on the 'Filesystem' provider failed"

| Type | Detail |
| --- | --- |
| Problem | Upon launching OPSWAT Central Management (such as on system startup), an error dialog for OCHelper.exe pops up. The error is "Attempting to perform the InitializeDefaultDrives operation on the 'Filesystem' provider failed" |
| Cause | PowerShell detectes that one or more mapped drives are not currently reachable. |
| Troubleshooting | Check if a system has one or more disconnected mapped drives. |
| Solution | Reconnect or disconnect the mapped drives. |

When OPSWAT Central Management is launched, specifically its tray icon process OCHelper.exe, an error dialog like in the image below pops up.

OCHelper is a PowerShell-based scripted process used to generate a tray icon GUI. The error "Attempting to perform the InitializeDefaultDrives operation on the 'Filesystem' provider failed" is a known PowerShell issue where it attempts to initialize connections to all mapped drive in the system before executing the main script but there are one or more mapped drives that cannot be reached. However, this error does not actually impede OCHelper.exe's function.

To stop this error dialog, you must either resolve any issues that cause the mapped drives to be disconnected in the first place or just disconnect the problematic drives from the system.

Alternatively, as OCHelper.exe only functions as a tray icon and is otherwise not vital to OPSWAT Central Management's operation, you can end this process via Windows's task manager. OPSWAT Central Management's service can still be managed via Windows Service management console (services.msc).
