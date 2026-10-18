<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/how-to-scan-windows-client-smb-shares -->

# How to scan Windows client SMB shares?

> **Info**
>
> Windows client shares are **not officially supported**. This document is intended solely for demonstration, testing, and proof-of-concept (PoC) purposes to help you learn how to scan them. It is not suitable for use in production environments.

> **Check Your Version:**
>
> This article applies to the legacy SMB service only: Linux deployments that use the `smb_legacy` module, and Windows deployments with `USE_OPSWAT_SMB_SERVICE=false`. The default SMB service on Windows (4.5.0 and later) and on Linux (4.6.0 and later) does not use `SMBSERVICE_SESSIONS_ON_STORAGE`.

## Symptoms

When the connection limit is reached, the following error will appear in SMB service logs:

```markdown
No more connections can be made to this remote computer at this time because the computer has already accepted the maximum number of connections. (3221225680) STATUS_REQUEST_NOT_ACCEPTED: 0xc00000d0
```

## Solution

When SMB shares are configured on a Windows client (Windows 10, Windows 11) there is a limit of connections that the SMB server allows. By default the limit is a total of 20 connections.

With its default configuration, the legacy SMB service can open up to 50 connections to the SMB server. However, it is possible to adjust certain configurations on the MDSS side to accommodate scenarios where fewer connections are necessary.

First, check how many connections are used by clients other than MDSS. You can check this using the following command that should be executed on the SMB Server with Administrative privileges

```powershell
Get-SMBSession
```

It will return a list of open sessions connections. Based on the number of connections you can adjust the [custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) using an environment variable called **SMBSERVICE_SESSIONS_ON_STORAGE** not have more than 20 connections used on the SMB Server.

> **Info**
>
> The legacy SMB service runs 5 processes, and each can open up to **SMBSERVICE_SESSIONS_ON_STORAGE** connections (default 10), which results in 50 connections.
>
> For Windows clients SMB shares, the recommendation is to configure **SMBSERVICE_SESSIONS_ON_STORAGE** to 2 or 3, but it depends of the number of connections already present.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
