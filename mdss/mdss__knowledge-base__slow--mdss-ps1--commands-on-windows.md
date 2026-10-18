<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/slow--mdss-ps1--commands-on-windows -->

# Slow 'mdss.ps1' commands on Windows

**Applies to:** MetaDefender Storage Security 4.5.2 and later, installed on Windows Server.

## Symptoms

- `mdss.ps1 -c restart` takes about 10 minutes instead of 1 to 2 minutes.
- `mdss.ps1 -c load-ca` and other `mdss.ps1` commands take 1 to 2 minutes.
- Every PowerShell script in `<install folder>\scripts` waits about 50 seconds before it starts. No error is logged and the scripts complete normally.

## Cause

Starting with MDSS 4.5.2, the PowerShell scripts shipped with MDSS are digitally signed. When a Software Restriction Policy (SRP) is applied to the server through Group Policy, even with the default security level "Unrestricted", Windows verifies the signature of every script before PowerShell runs it. Part of that verification is online:

- a revocation check of the signing certificate against DigiCert (OCSP and CRL), and
- a refresh of Microsoft's trusted-root and disallowed-certificate lists from `ctldl.windowsupdate.com`.

If the server cannot reach these hosts and the firewall silently drops the connections, every attempt runs to its timeout: about 20 seconds for the revocation check and 2 x 15 seconds for the Microsoft lists, about 50 seconds per script. MDSS runs many scripts per command, so the waits add up to minutes.

## Confirm

Run in an elevated PowerShell on the MDSS server. Adjust the path to your install folder.

```powershell
Measure-Command { [System.Management.Automation.Security.SystemPolicy]::GetLockdownPolicy("C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts\init.ps1", $null) }
```

Expected: under 1 second. If `TotalSeconds` is in the tens, this article applies.

Optional checks:

```powershell
reg query "HKLM\SOFTWARE\Policies\Microsoft\Windows\Safer\CodeIdentifiers"
Test-NetConnection ocsp.digicert.com -Port 80
Test-NetConnection ctldl.windowsupdate.com -Port 80
```

If the registry key exists, an SRP is applied to the server. `TcpTestSucceeded : False` after a long wait means the firewall drops the connection.

## Resolution (recommended)

Allow outbound HTTP (TCP port 80, not 443) from the MDSS server to:

- `ocsp.digicert.com`
- `crl3.digicert.com`
- `crl4.digicert.com`
- `cacerts.digicert.com`
- `ctldl.windowsupdate.com`

The checks then complete in milliseconds and Windows caches the results.

## Workaround for servers without Internet access

Both changes only stop Windows from waiting for connections that fail anyway. Validated on Windows Server 2025 with MDSS 4.5.2.

1. Stop the Microsoft certificate-list downloads. In an elevated command prompt:

   ```plaintext
   reg add "HKLM\SOFTWARE\Policies\Microsoft\SystemCertificates\AuthRoot" /v DisableRootAutoUpdate /t REG_DWORD /d 1 /f
   reg add "HKLM\SOFTWARE\Policies\Microsoft\SystemCertificates\AuthRoot" /v EnableDisallowedCertAutoUpdate /t REG_DWORD /d 0 /f
   ```
2. Make the DigiCert lookups fail immediately. Add these lines to `C:\Windows\System32\drivers\etc\hosts`, then run `ipconfig /flushdns`:

   ```plaintext
   0.0.0.0 ocsp.digicert.com
   0.0.0.0 crl3.digicert.com
   0.0.0.0 crl4.digicert.com
   0.0.0.0 cacerts.digicert.com
   ```

   This step has no effect if the server uses a WinHTTP proxy. Check with `netsh winhttp show proxy`.
3. Open a new PowerShell window and run the command from **Confirm** again. Expected: well under 1 second. No reboot is needed. MDSS picks up the change at the next `mdss.ps1 -c restart`.

Note: Microsoft recommends keeping the disallowed-certificate list update enabled. On a server without Internet access that update cannot run anyway. If you later allow the access, revert the workaround so the updates resume.

## Revert the workaround

```plaintext
reg delete "HKLM\SOFTWARE\Policies\Microsoft\SystemCertificates\AuthRoot" /v DisableRootAutoUpdate /f
reg delete "HKLM\SOFTWARE\Policies\Microsoft\SystemCertificates\AuthRoot" /v EnableDisallowedCertAutoUpdate /f
```

Remove the four lines from the hosts file and run `ipconfig /flushdns`.

## Reference

- Microsoft: [Configure trusted roots and disallowed certificates](https://learn.microsoft.com/en-us/windows-server/identity/ad-cs/configure-trusted-roots-disallowed-certificates)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
