<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/required-ftp-server-configuration -->

# Configuring a Windows IIS FTP Server for MDSS Scanning

**Applies to:** Microsoft IIS FTP on Windows Server · All MetaDefender Storage Security (MDSS) versions

MDSS scans FTP storage by opening a new passive data connection for every folder listing and every file it reads. One IIS setting governs how many of those connections the server can sustain — and its default is far too small for a scan. This page covers that setting, the connection limits that go with it, and how to verify the result.

---

## 1. Settings at a glance

Four server-side settings matter. Only the first one commonly breaks scans; the rest are usually already correct and just need confirming.

| Setting | Recommended | IIS default | Priority |
| ---- | ---- | ---- | ---- |
| Data Channel Port Range | `10000-20000` | `0-0` (ephemeral) | **Must set** |
| Firewall rule for that range | Inbound TCP allow | none | **Must set** |
| Server Listen Backlog | `500` | `60` | Confirm |
| Max Connections | unlimited, or >= 200 | `4294967295` | Confirm |

> **Read this first**
>
> When an FTP scan fails, **Max Connections and Server Listen Backlog are the settings everyone checks, and they are almost never the cause** — IIS ships with Max Connections effectively unlimited. The setting that actually stops scans is the passive **Data Channel Port Range**, because it is consumed by connection turnover rather than by how many clients are connected. Check it first.

---

## 2. Set the data channel port range

Every listing and every file transfer takes one port from this range. When the transfer finishes, Windows holds that port in `TIME_WAIT` for 120 seconds before it can be reused. A range of a handful of ports therefore supports only a handful of operations every two minutes, which a scan exhausts in seconds.

This range is server-wide — one range covers every FTP site on the machine. Run all commands in an **elevated** PowerShell session on the FTP server.

```powershell
& "$env:windir\system32\inetsrv\appcmd.exe" set config -section:system.ftpServer/firewallSupport `
  /lowDataChannelPort:10000 /highDataChannelPort:20000
```

Choosing your own numbers is fine, as long as they satisfy all four constraints:

- **At least 1000 ports** — see [How many ports you need](#6-how-many-ports-you-need).
- **Within 1025-65535** — IIS rejects anything lower.
- **Below 49152**, so the range never overlaps the Windows dynamic port range. Confirm your own with `netsh int ipv4 show dynamicport tcp`.
- **Clear of reserved and in-use ports.** Hyper-V, Docker and WinNAT silently reserve large blocks; a range overlapping one will fail to bind.

Check the range you picked is free:

```powershell
netsh int ipv4 show excludedportrange protocol=tcp

Get-NetTCPConnection -State Listen |
  Where-Object { $_.LocalPort -ge 10000 -and $_.LocalPort -le 20000 } |
  Select-Object LocalPort, @{n='Process';e={(Get-Process -Id $_.OwningProcess).ProcessName}}
```

No overlapping exclusions and no listeners returned means the range is yours to use.

---

## 3. Allow the range through the firewall

Widening the range achieves nothing if the firewall still blocks it. Scope the rule to the MDSS host so you are not opening 10,000 ports to the whole network.

```powershell
New-NetFirewallRule -DisplayName "IIS FTP Passive Data Channel 10000-20000 (MDSS)" `
  -Direction Inbound -Action Allow -Protocol TCP -LocalPort 10000-20000 `
  -RemoteAddress 10.0.0.50 -Profile Any
```

> **Use the MDSS host address, not the container address**
>
> The MDSS FTP services run in Docker, and their outbound traffic is source-NAT'd to the Docker host. The address to allow is the **MDSS host** IP — never the internal `172.x.x.x` container address.

To read the address the FTP server actually sees, run this while a scan or a storage **Test connection** is in progress:

```powershell
Get-NetTCPConnection -LocalPort 21 -State Established |
  Select-Object -ExpandProperty RemoteAddress -Unique
```

If the MDSS host uses DHCP, give it a static address or a reservation first — otherwise the rule silently stops matching the next time the lease changes.

For multiple MDSS hosts, `-RemoteAddress` accepts a list (`@('10.0.0.50','10.0.0.51')`) or a subnet (`'10.0.0.0/24'`). Scope the existing port 21 rule the same way — there is little point restricting the data channel while the control channel accepts connections from anywhere.

---

## 4. Confirm the connection limits

These two settings live on the FTP site rather than the server. Max Connections caps how many clients may be connected at once; Server Listen Backlog caps how many connection attempts can queue while the service is busy. MDSS connects in bursts, so a small backlog causes intermittent failures under load.

Substitute your own FTP site name:

```powershell
$site = "Your FTP Site Name"

& "$env:windir\system32\inetsrv\appcmd.exe" set site /site.name:"$site" `
  /ftpServer.connections.maxConnections:4294967295 `
  /ftpServer.connections.serverListenBacklog:500
```

`4294967295` is the IIS value for unlimited and is the default, so in most cases this command changes nothing but is harmless to run. Set it explicitly if a previous administrator lowered it. If your policy requires a real cap, size it to at least **200**: MDSS runs three services that each maintain their own connection pool, and a single host can hold up to 48 sessions before you account for retries or a second MDSS instance.

If `appcmd` rejects the syntax on your IIS version, set the same two values through **IIS Manager → select the FTP site → Advanced Settings → ftpServer → connections**.

### If the FTP server is behind NAT

The server tells the client which address to open the data connection on. Behind NAT it will advertise its private address unless you tell it otherwise, and every data connection will fail.

```powershell
& "$env:windir\system32\inetsrv\appcmd.exe" set config -section:system.applicationHost/sites/siteDefaults `
  /ftpServer.firewallSupport.externalIp4Address:"203.0.113.10"
```

Use the address MDSS connects to. Any intervening firewall must also forward the same data channel port range.

---

## 5. Restart and verify

IIS only picks up a changed data channel range when the FTP service restarts. This drops any FTP session in progress, so do it outside a scan window.

```powershell
net stop ftpsvc
net start ftpsvc

Get-Service ftpsvc | Select-Object Name, Status

Select-String -Path "$env:windir\system32\inetsrv\config\applicationHost.config" `
  -Pattern 'firewallSupport|maxConnections|serverListenBacklog|externalIp'
```

The service should report `Running`, and the configuration should show your new `lowDataChannelPort` and `highDataChannelPort`.

Now start a scan from MDSS and, while it runs, confirm data connections are landing in the new range:

```powershell
Get-NetTCPConnection | Where-Object { $_.LocalPort -ge 10000 -and $_.LocalPort -le 20000 } |
  Group-Object State | Format-Table Name, Count
```

A healthy result shows a handful of `Established` connections and a larger, **stable** count of `TimeWait` entries. Stable is the important word: a count that plateaus means ports are being recycled as fast as they are consumed. A count that climbs steadily toward the size of your range means the range is too small — widen it.

---

## 6. How many ports you need

Port demand is driven by connection turnover, not by how many files the storage holds:

```plaintext
ports needed  ~=  new data connections per second  x  120
```

The 120 is the Windows `TIME_WAIT` delay in seconds. A production MDSS scan measured roughly six new data connections per second, which held about 750 ports in use at steady state — against an IIS default that often leaves only a handful available.

| Deployment | Range | Ports |
| ---- | ---- | ---- |
| Single MDSS host, light scanning | `10000-11000` | 1001 |
| Standard — recommended default | `10000-20000` | 10001 |
| Multiple MDSS hosts, or real-time plus on-demand | `10000-20000` with a shorter `TIME_WAIT` | 10001 |

A bigger range costs nothing — IIS does not reserve the ports, it just draws from the range on demand.

For the heaviest workloads you can instead attack the other half of the formula and shorten `TIME_WAIT`, which multiplies the capacity of whatever range you chose:

```powershell
New-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters' `
  -Name 'TcpTimedWaitDelay' -PropertyType DWord -Value 30 -Force
```

---

## 7. If scans still fail

A misconfigured data channel produces this error in the MDSS FTP discovery log, usually preceded by several `Transient FTP error detected, retrying with fresh client` warnings a few seconds apart:

```text
System.IO.IOException: FTP passive data-channel connection to the server failed.
 ---> System.NullReferenceException: Object reference not set to an instance of an object.
   at FluentFTP.AsyncFtpClient.OpenDataStreamAsync(...)
```

The signature to recognise: logins succeed and the control channel works, but every data connection fails immediately. Work through these in order.

1. **Is the port range wide enough?** Run `appcmd list config -section:system.ftpServer/firewallSupport`. Anything under a few hundred ports is the cause.
2. **Did the FTP service restart** after the range changed? Without it, IIS is still using the old range.
3. **Does the firewall rule match the new range exactly,** and is it scoped to the right source address? A rule left pointing at an old narrow range fails identically.
4. **Watch the drops directly.** Enable logging, reproduce, then read it — dropped entries name the exact ports being refused.

```powershell
Set-NetFirewallProfile -All -LogBlocked True

# reproduce the failure, then:
Get-Content "$env:systemroot\system32\LogFiles\Firewall\pfirewall.log" -Tail 200 |
  Select-String 'DROP'

# turn logging back off when finished
Set-NetFirewallProfile -All -LogBlocked False
```

If the range and the firewall both check out, look at what the server advertises in its passive reply — a private or unexpected address there points back to the NAT setting in section 4. The IIS FTP logs under `%SystemDrive%\inetpub\logs\LogFiles\FTPSVC<n>` record every command, and the `sc-win32-status` column on failing `LIST` entries gives the underlying Windows error.

---

## 8. MDSS-side settings

Both of these are optional and read from the MDSS `.env` file. Neither is a substitute for the server configuration above, and both need `docker compose restart ftp-services` to take effect.

| Variable | Default | Guidance |
| ---- | ---- | ---- |
| `FTP_MAX_CONNECTIONS` | unset | Unset, each service starts at 3 connections and grows to a maximum of 16. Set it only when the FTP server genuinely limits concurrent sessions; lowering it does not relieve data channel port exhaustion. |
| `FTP_LIST_USE_STAT` | `false` | Leave off for IIS. It moves listings onto the control channel, but returns zero items against IIS FTP — discovery appears to succeed while finding nothing. |

---

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
