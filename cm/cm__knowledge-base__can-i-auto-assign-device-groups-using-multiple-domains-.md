<!-- source: https://www.opswat.com/docs/cm/knowledge-base/can-i-auto-assign-device-groups-using-multiple-domains- -->

# Can I Auto-Assign Device Groups Using Multiple Domains?

> **Check Your Version:**
>
> This article applies to all MetaDefender Endpoint deployed using My OPSWAT Central Management.

## Issue:

Device groups can currently only be auto-assigned using a single domain.

## Resolution:

If you need to assign device groups using a different domain, you will need to create a separate policy for that group.

![](https://uploads.developerhub.io/prod/1yda/wzt2sgmlq55p7o5n4qr46d0c55vy702m7q7n67snuykj08dk72ogcdeabjyekoz6.png)

**Example:**

Domain A → Group 1 (auto-assigned)

Domain B → Group 2 (requires a separate policy)

This ensures that devices are grouped correctly based on their domain, but each domain will require its own dedicated policy.

## Workarounds:

Create a separate policy for each domain to assign device groups.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
