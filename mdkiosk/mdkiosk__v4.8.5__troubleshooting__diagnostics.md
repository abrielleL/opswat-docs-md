<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics -->

# Diagnostics

# [Diagnostics](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#diagnostics)

Available starting in Kiosk 4.8.5, the **Diagnostics** section of the Kiosk Web Management Console runs a set of automated checks across connectivity, networking, services, system resources, licensing, scanning engines, certificates, and upgrade readiness — and lets you fix many common problems with a single click, right from the results.

## [Prerequisites](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#prerequisites)

- MetaDefender Kiosk 4.8.5 or later.
- Administrator access to the Kiosk Web Management Console.

## [Using Diagnostics](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#using-diagnostics)

1. Sign in to the Kiosk Web Management Console as an administrator.
2. In the left navigation, select **Diagnostics**.

Diagnostics runs its checks automatically and organizes the results into cards, each covering a related area of the product:

| Card | What it checks |
| --- | --- |
| Connections | Reachability of My OPSWAT, your primary and backup MetaDefender Core servers, Managed File Transfer, Active Directory, single sign-on, email (SMTP), and syslog. Also lets you run an on-demand connection test against any of these. |
| Network | Network adapters, DNS, internet access, proxy configuration, Windows Firewall, and the ports Kiosk needs. Also lets you capture network traffic for troubleshooting. |
| Kiosk Services | The status of the Kiosk application services, MetaDefender Core services, and the services used to read Mac/Linux-formatted media. |
| System | CPU and memory usage, available disk space, download bandwidth limits, recent crashes, installed programs, and the integrity of the installed application files. |
| License | Kiosk and MetaDefender Core license status, with warnings before a license expires. |
| Scanning Engines | Whether your scanning engines are running and up to date. |
| Certificates | The status of the certificate used to secure the Web Management Console. |
| Upgrades | Readiness for a Kiosk software upgrade, and — on a hardened image — readiness for an image upgrade. |
| Image & BIOS | BIOS version, device drivers, USB ports, and BitLocker status on the system drive. |

Each check shows a clear status along with a short description of what it found. A check that doesn't apply to your setup — for example, an image-upgrade check on a device that isn't a hardened image — is shown as **Not applicable** rather than a pass or fail.

## [Running a connection test](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#running-a-connection-test)

To investigate a specific connectivity problem:

1. Open the **Connections** card.
2. Choose the target you want to test — for example, MetaDefender Core or your Managed File Transfer server.
3. Run the test.

The test checks the connection step by step: whether the target can be found on the network, reached, connected to securely, and successfully responds, and finally whether your credentials are accepted. If an early step fails — for example, the target can't be reached at all — the later steps are shown as **Not applicable** instead of separate failures, so you're not misled into thinking there's a credentials problem when the real issue is network reachability.

## [Capturing network traffic](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#capturing-network-traffic)

If a network issue needs deeper investigation:

1. Open the **Network** card.
2. Start a capture. By default, only packet headers are recorded; you can choose to capture full payloads if you need more detail.
3. The capture is saved automatically and included the next time you generate a support package, so you don't need a separate step to hand it to OPSWAT support.

## [Fixing an issue](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#fixing-an-issue)

When Diagnostics finds a problem it can resolve directly, the relevant card offers a fix button. Available fixes include:

- Restarting Kiosk services that have stopped.
- Force-restarting a Kiosk service that's stuck (note: this ends any scan currently in progress on that service).
- Restarting MetaDefender Core.
- Restarting the services used to mount Mac/Linux-formatted media.
- Repairing the Kiosk installation.
- Cleaning up old temporary files.
- Removing a download bandwidth limit.
- Applying recommended settings to help prevent system crashes (this may require a restart to take effect).
- Disabling hibernation.
- Disabling Intel Graphics Command Center.

After you apply a fix, Diagnostics automatically checks again so you can confirm right away whether it worked.

Some issues aren't something Diagnostics can fix directly — for example, a license nearing expiration, an outdated scanning engine, or a certificate problem. In these cases, the card links you straight to the page where you can address it, instead of showing a fix button that wouldn't do anything.

## [Example](/docs/mdkiosk/v4.8.5/troubleshooting/diagnostics#example)

An administrator gets a report that a Kiosk can't reach MetaDefender Core. They open **Diagnostics** and see the Core entry in the **Connections** card reporting a failure. Running a connection test against Core shows the check stopping at the network-reachability step, with the later steps (secure connection, response, credentials) shown as Not applicable. This tells the administrator the issue is a network or firewall problem, not an incorrect login or API key — saving time that would otherwise go into checking credentials that were never the problem.

Note

Diagnostics reflects the state of your Kiosk at the moment each check runs. If you make a change elsewhere in the Console, revisit Diagnostics (or apply a fix, which re-checks automatically) to see updated results.
