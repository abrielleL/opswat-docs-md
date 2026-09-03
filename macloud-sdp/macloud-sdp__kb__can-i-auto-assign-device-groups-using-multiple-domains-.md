<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/can-i-auto-assign-device-groups-using-multiple-domains- -->

# Can I Auto-Assign Device Groups Using Multiple Domains?

This article applies to all MetaDefender Endpoint deployed using MetaDefender IT Access.

## [Issue:](/docs/macloud-sdp/kb/can-i-auto-assign-device-groups-using-multiple-domains-#issue)

Device groups can currently only be auto-assigned using a single domain.

## [Resolution:](/docs/macloud-sdp/kb/can-i-auto-assign-device-groups-using-multiple-domains-#resolution)

If you need to assign device groups using a different domain, you will need to create a separate policy for that group.

**Example:**

Domain A → Group 1 (auto-assigned)

Domain B → Group 2 (requires a separate policy)

This ensures that devices are grouped correctly based on their domain, but each domain will require its own dedicated policy.

## [Workarounds:](/docs/macloud-sdp/kb/can-i-auto-assign-device-groups-using-multiple-domains-#workarounds)

Create a separate policy for each domain to assign device groups.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
