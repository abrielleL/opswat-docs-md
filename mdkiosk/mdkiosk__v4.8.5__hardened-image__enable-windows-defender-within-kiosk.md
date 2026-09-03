<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/hardened-image/enable-windows-defender-within-kiosk -->

# Enable Windows Defender within Kiosk

Kiosk can detect Windows Defender. In such a case, Kiosk will add an exclusion list, which is all volume characters from C to Z. The exclusion list will prevent Windows Defender from scanning and quarantining files from USB.

In a domain joined computer, the administrator could configure tamper protection to protect security settings. Kiosk will not have the ability to change the exclusion list of Windows Defender.

You can check the status of Windows Defender tamper protection by the following PowerShell command.

> `Get-MpComputerStatus | Select-Object -ExpandProperty TamperProtectionSource`

If it returns "Signatures", it means the tamper protection is controlled by local source and could apply changes from local.
