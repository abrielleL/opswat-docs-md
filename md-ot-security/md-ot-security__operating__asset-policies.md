<!-- source: https://www.opswat.com/docs/md-ot-security/operating/asset-policies -->

# Asset Policies

First, users need to select a sensor from the list at the top-right corner.

The **Asset Policies** tab is accessible by clicking on icon Policies on footer menu.

The asset policies contains all policies of the asset that learnt by MetaDefender OT Security or manually create by user.

There is 5 type of asset policies:

- Allow list.
- Blocklist:

  - Unauthorized asset.
  - Misconfiguration.
  - Supply chain violation.
  - Vulnerability.
  - Firmware Changes
  - Port Scan Rules

If the asset violates both allowlist and blocklist at the same time, blocklist detection will have higher priority.

The policies in the allowlist will be highlighted if they have the same rule as the misconfiguration blocklist policies.
