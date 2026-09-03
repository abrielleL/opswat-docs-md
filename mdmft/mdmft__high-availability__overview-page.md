<!-- source: https://www.opswat.com/docs/mdmft/high-availability/overview-page -->

# Overview Page

Summarize Page    Connect to Cursor Connect to VS Code

The Overview page provides a live health monitor that periodically polls all configured MetaDefender® MFT nodes and cluster peers.

High Availability Configuration Tool with fully configured cluster

Info

Note, that after a new installation, only the Node Health Cards placeholders are visible, as the Cluster mode is disabled by default.

High Availability Configuration Tool after a new installation - not configured yet

### [Node Health Cards](/docs/mdmft/high-availability/overview-page#node-health-cards)

Each configured MetaDefender® MFT node is displayed as a card showing:

| Field | Description |
| --- | --- |
| **Name** | The node's display name (e.g. "MFT1") |
| **Status** | Color-coded indicator:  🟢 Active  🟠 Passive  🔴 Unhealthy  ⚪ Unreachable. |
| **Version** | The software version reported by the node's health endpoint |
| **Address** | The Node Manager URL |
| **Last Checked** | Timestamp of the most recent health check |

### [Peer Health Cards](/docs/mdmft/high-availability/overview-page#peer-health-cards)

Peer health cards are only visible when **cluster mode is enabled** (more than one peer configured). Each peer card shows:

| Field | Description |
| --- | --- |
| Display name | Peer identifier, with `(Self)` badge for the local peer. |
| Health status | Color-coded health indicator:  🟢 Healthy  🔴 Unhealthy  ⚪ Unreachable |
| Role | Leader or Follower (Raft consensus role) |
| Address | The peer's HTTP address |
| Last checked | Timestamp of the most recent health check |
| Error Details | Appears when the peer is unhealthy or unreachable. |
