<!-- source: https://www.opswat.com/docs/md-ot-security/operating/connection-policies -->

# Connection Policies

The **Connection policies** tab is accessible by clicking on the icon Policies in the footer menu.

**Connection policies** is a set of rules for connections between source and destination devices.

**Connection policy** works based on a combination of both ***allowlist*** and ***blocklist*** principles.

There is 4 type of connection policies:

- Allow list.
- Block list:

  - Unauthorized connection.
  - Disallowed Port/Period.
  - Disallowed Country of Remote Host.

If the connection violates both allowlist and blocklist at the same time, blocklist detection will have higher priority.

The policies in allowlist will be highlighted if they have the same rule with blocklist policies.
