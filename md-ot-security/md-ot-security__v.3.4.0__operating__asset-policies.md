<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/asset-policies -->

# Asset Policies

The **Asset policies** tab is accessible by clicking on icon Policies on footer menu.

The asset policies contain all policies of the asset that learnt by MetaDefender OT Security or manually create by user.

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

The policies in allowlist will be highlighted if they have the same rule with misconfiguration blocklist policies.
