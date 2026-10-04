<!-- source: https://www.opswat.com/docs/metadefender-ot-access/metadefender-ot-access-installation-and-administration-guide/high-availability -->

# High Availability

## 1. Overview

High Availability (HA) runs MetaDefender OT Access as a **failover pair**: two appliances on the same software version. One is the **Primary**, the other the **Backup**, which the page labels *STANDBY*.

- The **Primary** serves all traffic: the web portal, the Windows app gateway, and every SSH/RDP/VNC session.
- The **Backup** keeps a live copy of the database (streaming replication) and receives the configuration and recordings on a schedule. It does not serve users. Its portal on port 443 is intentionally closed while it is the backup.
- Clients never connect to a node by its own address. They use two **Shared IPs**, also called VIPs, and whichever node is primary holds both:

  - **Management VIP** — the address of the web portal (port 443) and the setup web (port 8443).
  - **Service VIP** — the address the Windows app (MetaDefender OT Access Console / Endpoint) signs in against on port 443. Opening it in a browser returns nothing; that is expected.
- **Automatic failover.** If it is enabled, and the primary stops sending heartbeats for longer than the configured timeout, the backup promotes itself and takes the Shared IPs.
- You can also hand the role over deliberately (**Switch over**), take an appliance out of the pair (**Unpair**), or add one (**Pair**).

You manage all of this from the **setup web** of each appliance (port 8443), under **Configuration → High Availability**.

About the timings in this guide

This guide describes build **2.4.0.15384**. Timings are indicative and depend on your data volume and network.

## 2. Use cases

Find your goal, then work through the listed sections in that order.

| I want to… | Sections to follow, in order |
| --- | --- |
| **Set up failover** for an appliance that runs on its own today. | 1. Configure the Shared IPs (section 5). 2. Pair the backup (section 6). 3. Verify the pair (section 7). 4. Point users at the Shared IPs, not at the node addresses. |
| **Patch, reboot or service the primary** without losing the service. | 1. Verify the pair (section 7). 2. Switch over (section 8). 3. Do the maintenance on the node that is now the backup. 4. Switch over again if you want the role back (section 8). |
| **Take over after the primary died** and automatic failover did not fire. | 1. Force to primary on the backup (section 8). 2. Pair the old primary back in as the new backup (section 6), then verify (section 7). |
| **Remove an appliance** from the pair: retire, relocate, rebuild, or stop using failover. | 1. If it is the current primary, switch over first (section 8). 2. Unpair it, signed in on that node (section 9). |
| **Rebuild a backup** that is out of sync and cannot be trusted. | 1. Unpair it (section 9). 2. Pair it again (section 6), then verify (section 7). |

### Which address do I give to whom?

- **Users, browsers and the Windows app — always the Shared IPs**, never a node's own address. This is what makes a failover invisible to them: the address they use does not change when the roles swap.

  - Portal users → Management VIP.
  - Windows app → Service VIP.
- **Administrators — the node's own setup web on port 8443**, because every HA action runs on one specific node. Working from the primary is usually the right choice: its page shows both nodes.

## 3. Before you begin

### What you need

- **Two appliances on the same software version** — one primary, one backup.

  - The pairing wizard checks the version. Do not pair mismatched builds.
  - Pairing replaces everything on the backup (configuration, users, sessions, recordings) with a copy of the primary, so it may still hold data when you start.
- **Two unused IP addresses in the appliances' subnet** for the Management VIP and the Service VIP. You enter them under **Traffic Redirection** (section 5).

### Good to know

- **Network.** The two appliances talk to each other on the ports below. Open them only if a firewall sits between the appliances.

  - `7008/tcp` — management, health checks, file synchronization.
  - `5432/tcp` — database replication.
- While a node is the backup, its portal (port 443) answers *502 Bad Gateway* and its setup-web sessions are short-lived. Manage the pair from the **primary**: its page shows both nodes.
- **The page does not update by itself after an HA action.** Reload it in the browser, or click **Refresh** in the Failover Pair header. Reloading also closes a dialog that stayed open, and no confirmed action is undone by it.
- Give each appliance a distinct hostname: the HA dialogs name the nodes by hostname, so identical names are hard to tell apart. Identical hostnames still work.

## 4. Open the High Availability page

1. Sign in to the setup web of the appliance: `https://<appliance-ip>:8443`.
2. In the left navigation, open **Configuration → High Availability**.

The page has four sections:

| Section | What it shows / does |
| --- | --- |
| **Failover Pair** | The topology: the Shared IPs, one card per node (role, status, version, sessions, last sync), the sync link between them, and the actions. On an unpaired appliance it shows the banner *"High availability is not configured"* and a **Pair an appliance** button. |
| **Traffic Redirection** | Method *SHARED*: the Management VIP and Service VIP addresses (CIDR) and the interface they are bound to. Must be identical on both nodes. |
| **Failover Behaviour** | **Automatic failover** on/off, **Heartbeat timeout** (seconds), **Synchronization interval** (minutes, for configuration and recordings) and the **Network connectivity tests** address list. |
| **Failover History** | Role changes, lost and recovered peer connections, conflict resolutions, and file-synchronization entries, from both nodes, newest first. |

## 5. Configure the Shared IPs and the failover behaviour

Do this on the appliance that will be the **primary**, before pairing.

1. Expand **Traffic Redirection**.
2. Enter the **Management VIP address** in CIDR form and pick its **Interface**.
3. Enter the **Service VIP address** the same way and its interface.
4. Click **Save**. The VIP interface must be the same on every node of the pair.
5. Expand **Failover Behaviour** and review:

   - **Automatic failover** — leave enabled unless you want to promote the backup manually only. The summary line reads *Automatic* or *Manual* so you can tell the mode at a glance.
   - **Heartbeat timeout** — how long the backup waits before declaring the primary dead. Default 30 seconds.
   - **Synchronization interval** — how often the primary copies configuration and recordings to the backup. Default 5 minutes. The database replicates continuously regardless of this value.
6. Click **Save**.

## 6. Pair a backup appliance

Run the wizard on the appliance that will stay the **primary**. The other appliance must be reachable, on the same version, and must hold no data you want to keep.

1. On the primary, open **Configuration → High Availability** and click **Pair an appliance** (in the banner, or on the empty *BACKUP · Not configured* card).
2. **Step 1 — Connect.** Enter the **Backup appliance address** and leave **Port** at `7008`. Click **Connect**.
3. **Step 2 — Verify identity.** The wizard shows three checks:

   - **Appliance reachable** — `host:7008`.
   - **Software version** — must match this appliance.
   - **Certificate fingerprint (SHA-256)** — this is the HA certificate, not the web certificate. Confirm the value from the backup appliance itself, not only from this dialog, before you accept it. Skipping the check lets an impostor join the pair.
   - Tick *"The fingerprint above matches…"*, then click **Trust this appliance**.
4. **Step 3 — Authorize.**

   - **Administrator on backup** and **Password** — the account you use to sign in to the backup's own setup web (port 8443). The wizard uses it once and does not store it.
   - Tick *"I understand all existing data on the backup appliance will be erased"*.
   - Click **Pair & seed backup**.
5. **Wait.** The page shows *"Pairing accepted"*.

   - The wizard says the initial seed takes **10–20 minutes**, depending on the volume of recordings. The primary keeps serving.
   - The wizard dialog does not close by itself. Reload the page in the browser: that closes it and shows the new state. You do not need to click **Cancel** first, and reloading does not cancel the pairing.
6. **Verify the result with section 7 before you rely on the pair.** Pairing can finish with the roles assigned and the page green while the database stream never starts.

## 7. Verify the pair is healthy

Do this after every pairing, and again after every failover or switchover. On the primary's High Availability page:

| Check | Healthy | Needs attention |
| --- | --- | --- |
| Primary card | **PRIMARY · Running · serving traffic**, **LAST SYNC** "A moment ago" | LAST SYNC *N/A* for more than a few minutes: the backup is not streaming from this node |
| Backup card | **STANDBY**, and **DATA RECEIVED** "A moment ago" or a few minutes | *Unreachable*, *Database unreachable*, or DATA RECEIVED *N/A* |
| Link between the cards | Green *Synchronizing · config - recordings* | Amber or grey link |
| Failover History | *"Config synced successfully"* from **both** nodes at every synchronization interval | Repeated *"Lost connection to peer"*, *"Conflict detected: both nodes are primary"* |
| Shared IPs | The portal opens on the Management VIP; the Windows app signs in on the Service VIP | Portal or app unreachable on the VIP while a node's own address works |

Green does not mean replicating

The green *Synchronizing* link and the *Warm · ready to take over* label come from the node's role alone, not from the database stream. A pair can sit with both labels green and no replication at all.

In normal operation, **LAST SYNC** and **DATA RECEIVED** keep moving forward. If either stops updating, or stays *N/A*, the database stream between the two appliances is not established, whatever the rest of the page shows.

A backup in that state is still eligible for automatic failover. If the primary then fails, the backup is promoted and serves the data it last received, and the page gives no warning that the data is out of date.

Treat the two **sync timestamps** as the only reliable indicator of replication.

### If the timestamps stop updating

Treat the pair as not protecting you. Unpair the backup (section 9), pair it again (section 6), and repeat the checks above. If the timestamps still do not move, contact OPSWAT Support before you rely on the pair.

## 8. Switch over: demote the primary to backup

A **switchover** is a planned, controlled role swap: the current primary synchronizes one last time, hands the role and the Shared IPs to the backup, and becomes the backup itself. Use it before maintenance of the primary (updates, reboots) or to move service back after a failover.

### Before you start

- The switchover disconnects every connected user. Sessions do not migrate; users reconnect to the same Shared IP once it points at the new primary.
- Check the pair is healthy first (section 7). Do not switch over to a backup whose DATA RECEIVED is *N/A*.
- Announce a short outage. The portal on the Management VIP is unreachable while the Shared IPs move to the new primary, and every portal session is lost.

### Steps

1. Sign in to the setup web of the **current primary** and open **Configuration → High Availability**.
2. On the card marked **PRIMARY (this node)**, click **Switch over to backup**.
3. Read the dialog `Switch over to <backup>`. It shows the direction (*CURRENT PRIMARY → BECOMES PRIMARY*) and the warning *"All sessions end"*. Nothing happens until you confirm: to leave without switching over, click **Cancel** or reload the page.
4. Tick *"I understand all active sessions will be disconnected."* and click **Switch over**.
5. After 15–30 seconds click **Refresh**. The card of this node now reads **STANDBY** and the other node **PRIMARY** with a new **ROLE SINCE** time. Continue on the new primary; your session on this node ends shortly.

The Windows app reconnects to the Service VIP by itself once the address moves, with no re-login.

### Force to primary

**Force to primary** promotes the backup by hand when the primary is gone. It appears on the backup's own card, and only while the peer is unreachable, so you must be signed in to the backup to use it.

Which failover mode you run decides whether you ever see it:

- **Automatic failover off.** The backup never promotes itself, so the action stays available until you use it. This is the normal recovery path in manual mode.
- **Automatic failover on, which is the default.** The backup promotes itself once the heartbeat timeout expires, about 30 seconds. The action appears in that gap and disappears again, so do not plan on clicking it. Wait for the promotion, then check section 7.

Before you confirm, the dialog warns that anything not synchronized since the last run is lost, and that the old primary must be rejoined by hand once it returns. Confirm the primary is really powered off: if it is only isolated from this appliance, both nodes will claim the role.

## 9. Unpair an appliance

**Unpair** removes *this* appliance from the pair and turns it back into a standalone appliance. The page offers the action only on the card of the node you are signed in to; to remove the backup, sign in to the backup.

1. Sign in to the setup web of the appliance you want to remove (normally the backup) and open **Configuration → High Availability**.
2. On the card marked **(this node)**, click **Unpair**.
3. Read the dialog `Unpair <hostname>`. Automatic failover, switchover and monitoring stop for this appliance immediately, and the appliance tells the peer to forget it. Both sides keep their sessions and recordings.
4. Tick *"I understand this appliance will leave the cluster and stop failing over."* and click **Unpair**.
5. Wait for the message *"Unpair operation completed."* and reload the page.

### Result

- **This appliance**: shows the banner *"High availability is not configured"* and a single *PRIMARY (this node)* card with *"No peer"*. It becomes a standalone appliance within about 30 seconds and its own portal on port 443 comes back. It keeps the Shared IP settings but does not take the addresses.
- **The remaining appliance**: also shows the not-configured banner and *"No peer — pair an appliance to enable failover"*. It keeps the Shared IPs and continues serving users.
- Both appliances now hold an independent copy of the data as of the moment of the unpair. Changes made on one are no longer copied to the other.

The card may lag behind

Immediately after the unpair the card may still read *STANDBY · Unreachable*. That is the last state fetched before the node re-initialised; reload the page.

## 10. Failover History

The **Failover History** section lists events from both nodes, newest first, with the node's hostname and IP. Scroll to load older entries.

| Entry | Meaning |
| --- | --- |
| *Config synced successfully* | A scheduled configuration/recordings sync completed (one entry per node per interval). Absence for longer than the interval means the sync is not running. |
| *Pulled N recording file(s) from peer …* | The appliance copied recordings across during a scheduled sync. |
| *Role changed to master / standby_leader / replica* | Database role changes on that node. |
| *Lost connection to peer … / Connection to peer … recovered* | Heartbeat between the nodes lost or restored. |
| *Promoted to primary after peer … was lost* | Automatic failover fired on that node. |
| *Conflict detected: both nodes are primary* and *Conflict resolution: …* | Both nodes believed they were primary. The watchdog demoted one of them. Check both sync timestamps afterwards, with section 7. |

What this log does not tell you

Failover History records role changes, peer connectivity and file synchronization. It does not record pairing, unpairing, or the initial seed, and it does not report the state of the database stream. Use the two sync timestamps in section 7 for that.
