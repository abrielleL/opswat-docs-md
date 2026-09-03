<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-to-resolve----client-device-is-not-known----error-in-uag- -->

# How to Resolve “Client Device Is Not Known” Error in UAG?

This article applies to all supported version of **VMware Horizon client.**

### [Problem Summary:](/docs/macloud-sdp/kb/how-to-resolve----client-device-is-not-known----error-in-uag-#problem-summary)

When users encountered the **“Your client device is not known and therefore cannot be checked for compliance with the service access policy.”** error when accessing the VM from Horizon environment. The error occurred across multiple device and network combinations, resulting in blocked access.

The issue was caused by the **"Unknown Endpoint" status being disabled** in the **VMware Unified Access Gateway (UAG)**. When this status is disabled, MetaAccess cannot identify unregistered devices, triggering the error.

### [Resolution Steps: Enable "Unknown Endpoint" Status in VMware UAG](/docs/macloud-sdp/kb/how-to-resolve----client-device-is-not-known----error-in-uag-#resolution-steps-enable-unknown-endpoint-status-in-vmware-uag)

1. Log in to the **VMware UAG admin console**.
2. Navigate to the **Integration** section or relevant policy handling endpoint checks.
3. Locate the setting labeled **“Unknown Endpoint”**.
4. Ensure that this option is **enabled**.

   - Enabling this allows MetaDefender IT Access to recognize and scan unknown devices, avoiding client rejection.

#### [Note:](/docs/macloud-sdp/kb/how-to-resolve----client-device-is-not-known----error-in-uag-#note)

Ensure the **MetaDefender Endpoint agent** on all client devices is up to date.

Update the **VMware Horizon client** and **UAG** to the latest supported versions for full compatibility.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
