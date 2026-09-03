<!-- source: https://www.opswat.com/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c -->

# Resolving error code 1722 when OPSWAT ONTAP Connector tries to connect to ONTAP AV Connector

## [Overview](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#overview)

This document describes a troubleshooting and resolution procedure for a scenario where the **OPSWAT ONTAP Connector** receives **RPC_S_SERVER_UNAVAILABLE (error 1722, 0x6BA)** when connecting to a named pipe on a hardened Windows Server, even though the pipe is confirmed to exist on the server.

The issue was observed against a server running NetApp ONTAP AV Connector, where the OPSWAT ONTAP Connector connects to the pipe `\\127.0.0.1\pipe\ntapvscp`. The same pattern applies to any same-host RPC-over-named-pipes integration that uses an SMB-style pipe path (`\\127.0.0.1\pipe\...`, `\\localhost\pipe\...`, or `\\<hostname>\pipe\...`).

## [Symptoms](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#symptoms)

The OPSWAT ONTAP Connector logs an entry similar to the following when the registration call fails:

[2026-05-06 11:23:49] [Error] [1722] VS_Registration2 failed

Additional indicators:

- The Win32 error code `1722` (`RPC_S_SERVER_UNAVAILABLE`) appears in the OPSWAT ONTAP Connector log.
- The named pipe is confirmed to exist on the server (visible under `\\.\pipe\`).
- The connection target is the loopback interface (`127.0.0.1`), so no network device or external firewall is involved.
- The host has been hardened according to a security baseline (CIS, STIG, or vendor-specific hardening).

## [Root Cause](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#root-cause)

Named-pipe access through an SMB-style path (for example `\\127.0.0.1\pipe\ntapvscp`) routes through the SMB redirector and requires:

1. A listener on TCP 445.
2. A valid inbound firewall rule allowing the connection.
3. SMB Server bound to a network interface (which is what creates the listener).

On a hardened host, all three of these layers are commonly disabled to reduce the attack surface. The combination produces the observed failure chain:

App opens \\127.0.0.1\pipe\ntapvscp
-> Routed through the SMB redirector
-> SMB attempts to connect to 127.0.0.1:445
-> No listener on 445
-> SMB returns ERROR_NETNAME_DELETED (64) or ERROR_UNEXP_NET_ERR (59)
-> RPC layer surfaces RPC_S_SERVER_UNAVAILABLE (1722)

Note that the AV Connector itself, the named pipe, and the local RPC subsystem are healthy. Only the SMB transport layer used to reach the pipe is broken.

## [Diagnostic Procedure](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#diagnostic-procedure)

Run the following commands in an elevated PowerShell session on the affected host.

### [1. Confirm the named pipe exists](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#1-confirm-the-named-pipe-exists)

PowershellCopyGet-ChildItem \\.\pipe\ | Where-Object Name -like "*ntapvscp*"
### [2. Confirm RPC over the local NPFS path works (bypasses SMB)](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#2-confirm-rpc-over-the-local-npfs-path-works-bypasses-smb)

rpcping -s . -t ncacn_np -e \pipe\ntapvscp -v 3

A successful result (`Completed 1 calls in N ms`) proves the pipe and the local RPC stack are healthy.

### [3. Reproduce the failure over the SMB path](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#3-reproduce-the-failure-over-the-smb-path)

rpcping -s 127.0.0.1 -t ncacn_np -e \pipe\ntapvscp -v 3

A failure with `Exception 1722` and an inner status of `0x40` (`ERROR_NETNAME_DELETED`) or `0x3B` (`ERROR_UNEXP_NET_ERR`) confirms the SMB path is broken.

### [4. Test TCP 445 reachability on loopback](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#4-test-tcp-445-reachability-on-loopback)

PowershellCopyTest-NetConnection 127.0.0.1 -Port 445

`TcpTestSucceeded : False` indicates nothing is listening on TCP 445.

### [5. Identify which layer is broken](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#5-identify-which-layer-is-broken)

PowershellCopy# Is the Server service running?
Get-Service LanmanServer, LanmanWorkstation
# Is anything listening on 445?
Get-NetTCPConnection -LocalPort 445 -State Listen
netstat -ano | findstr :445
# Is SMB Server bound to any network interface?
Get-SmbServerNetworkInterface
# What does the firewall rule for SMB-In look like?
Get-NetFirewallRule -DisplayName "File and Printer Sharing (SMB-In)" |
Format-Table DisplayName, Enabled, Profile
# Is "File and Printer Sharing for Microsoft Networks" bound to the active adapter?
Get-NetAdapterBinding -ComponentID ms_server
# What is the active network profile?
Get-NetConnectionProfile

A typical hardened-host signature is:

- `LanmanServer` is running.
- `Get-NetTCPConnection -LocalPort 445 -State Listen` returns nothing.
- `Get-SmbServerNetworkInterface` returns nothing.
- The `File and Printer Sharing (SMB-In)` firewall rule is `Enabled: False`.
- `Get-NetAdapterBinding -ComponentID ms_server` shows `Enabled: False` on the active adapter.

## [Resolution](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#resolution)

The fix restores SMB inbound on the host while keeping the customer's hardening intact for everything except loopback.

Run the following in an elevated PowerShell session:

PowershellCopy# 1. Enable the inbound firewall rule for SMB
Enable-NetFirewallRule -DisplayName "File and Printer Sharing (SMB-In)"
# 2. Scope the rule to loopback only (do not expose 445 on the network)
Set-NetFirewallRule -DisplayName "File and Printer Sharing (SMB-In)" -RemoteAddress 127.0.0.1
# 3. Re-bind "File and Printer Sharing for Microsoft Networks" to the active adapter
Enable-NetAdapterBinding -Name "Ethernet" -ComponentID ms_server
# 4. Restart the Server service so it picks up the new binding
Restart-Service LanmanServer -Force

If the active adapter is named something other than `Ethernet`, substitute the correct name from `Get-NetAdapterBinding -ComponentID ms_server`.

## [Verification](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#verification)

After applying the fix, run the following to confirm each layer is healthy:

PowershellCopy# Adapter binding restored
Get-NetAdapterBinding -ComponentID ms_server
# Expected: active adapter shows Enabled : True
# SMB Server bound to interface
Get-SmbServerNetworkInterface
# Expected: at least one row returned
# TCP listener up on 445
Get-NetTCPConnection -LocalPort 445 -State Listen
# Expected: LocalAddress :: , LocalPort 445, State Listen, OwningProcess 4
# Loopback reachability
Test-NetConnection 127.0.0.1 -Port 445
# Expected: TcpTestSucceeded : True
# SMB session establishment works
net use \\127.0.0.1\IPC$
# Expected: "The command completed successfully"
# RPC over the SMB path now works
rpcping -s 127.0.0.1 -t ncacn_np -e \pipe\ntapvscp -v 3
# Expected: Completed 1 calls in N ms

Once `rpcping` succeeds against the SMB path, reproduce the original failure with the OPSWAT ONTAP Connector. The connector should now open the pipe and complete the RPC call without `RPC server is unavailable`, and `VS_Registration2` should complete successfully.

## [Why This Happens on Hardened Hosts](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#why-this-happens-on-hardened-hosts)

Common hardening baselines disable inbound SMB to reduce lateral-movement risk. Typical changes include:

- Disabling the `File and Printer Sharing (SMB-In)` firewall rule for all profiles.
- Unchecking "File and Printer Sharing for Microsoft Networks" on every network adapter, which removes the binding the SMB Server uses to create its TCP 445 listener.
- Stopping or disabling the `LanmanServer` service.

Any one of these disables inbound SMB. The hardened host in this case had two of the three applied (the firewall rule and the adapter binding). The Server service was still running, but with no adapter binding it had nothing to listen on, so port 445 was effectively closed even on loopback.

## [Recommendations](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#recommendations)

### [For the customer](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#for-the-customer)

1. Document the exception in the host's hardening baseline. A subsequent hardening sweep applied through GPO, Intune, or a hardening tool will revert these settings unless the exception is encoded in the baseline.
2. Keep the firewall rule scoped to `127.0.0.1` only. This restores SMB exactly enough for same-host named-pipe IPC and does not expose port 445 to the network.
3. If an EDR product is present, verify it does not re-block SMB at the session layer. Some EDRs flag SMB sessions as lateral movement and reset them even when the OS allows the traffic.

## [Reference: Error Codes Encountered](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#reference-error-codes-encountered)

| Code | Hex | Name | Meaning |
| --- | --- | --- | --- |
| 1722 | 0x6BA | `RPC_S_SERVER_UNAVAILABLE` | Top-level RPC error surfaced to the client |
| 64 | 0x40 | `ERROR_NETNAME_DELETED` | The specified network name is no longer available (no SMB listener) |
| 59 | 0x3B | `ERROR_UNEXP_NET_ERR` | An unexpected network error occurred (SMB session/negotiation failure) |
| 1706 | 0x6AA | `RPC_S_NO_ENDPOINT_FOUND` | rpcping endpoint string formatted incorrectly (no real failure) |

## [Reference: rpcping Endpoint Syntax](/docs/mdss/where-to-get-help/resolving-error-code-1722-when-opswat-ontap-connector-tries-to-c#reference-rpcping-endpoint-syntax)

When `-s` already specifies the server, the `-e` argument must be the bare endpoint name without server prefix:

| Form | Result |
| --- | --- |
| `-s 127.0.0.1 -e \pipe tapvscp` | Correct (SMB path) |
| `-s . -e \pipe tapvscp` | Correct (local NPFS path) |
| `-s 127.0.0.1 -e \\.\pipe tapvscp` | Returns 1706 |
| `-s 127.0.0.1 -e \\127.0.0.1\pipe tapvscp` | Returns 1706 |
