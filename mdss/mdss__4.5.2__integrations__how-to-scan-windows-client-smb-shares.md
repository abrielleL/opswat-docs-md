<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/how-to-scan-windows-client-smb-shares -->

# How to scan Windows client SMB shares?

> **Info**
>
> Windows client shares are **not officially supported**. This document is intended solely for demonstration, testing, and proof-of-concept (PoC) purposes to help you learn how to scan them. It is not suitable for use in production environments.

## Symptoms

When the connection limit is reached, the following error will appear in SMB service logs:

```markdown
No more connections can be made to this remote computer at this time because the computer has already accepted the maximum number of connections. (3221225680) STATUS_REQUEST_NOT_ACCEPTED: 0xc00000d0
```

## Solution

When SMB shares are configured on a Windows client (Windows 10, Windows 11) there is a limit of connections that the SMB server allows. By default the limit is a total of 20 connections.

The default configuration of MetaDefender Storage Security (MDSS) requires a minimum of 50 connections to ensure optimal performance. However, it is possible to adjust certain configurations on the MDSS side to accommodate scenarios where fewer connections are necessary.

First, we should check how many connections are used excluding the 50 connections required by MDSS. You can check this using the following command that should be executed on the SMB Server with Administrative privileges

```powershell
Get-SMBSession
```

It will return a list of open sessions connections. Based on the number of connections you can adjust the [custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) using an environment variable called **SMBSERVICE_SESSIONS_ON_STORAGE** not have more than 20 connections used on the SMB Server.

> **Info**
>
> There are a total of 5 SMB services and each will use a number of **SMBSERVICE __*****SESSIONS***** ON_STORAGE** equal to 10 which results in 50 connections.
>
> For Windows clients SMB shares, the recommendation is to configure **SMBSERVICE_SESSIONS_ON_STORAGE** to 2 or 3, but it depends of the number of connections already present.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
