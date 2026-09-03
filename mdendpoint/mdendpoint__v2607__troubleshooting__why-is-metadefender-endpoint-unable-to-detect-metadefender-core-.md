<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/troubleshooting/why-is-metadefender-endpoint-unable-to-detect-metadefender-core- -->

# Why is MetaDefender Endpoint Unable to Detect MetaDefender Core and How to Fix It?

> **Check Your Version:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows.

When MetaDefender Endpoint cannot detect the MetaDefender Core application. This issue is caused by older versions of the MetaDefender Endpoint SDK that do not yet support MD Core detection.

This article explains the cause of the issue and the steps to resolve it.

## Root Cause

- Devices running older versions of MetaDefender Endpoint **7.6.2411** use an SDK version **4.3.4344** that does not support MD Core detection.
- Newer versions of MetaDefender Endpoint **7.6.2508** include SDK **4.3.4761.0 or higher**, which supports MD Core detection.

## Solution

To resolve this issue, upgrade the affected devices to a supported version of MetaDefender Endpoint:

1. **Upgrade MetaDefender Endpoint (MetaDefender Endpoint):**
   - Install the latest available version of MetaDefender Endpoint
2. **Verify the Upgrade:**
   - After upgrading, check the SDK version in MetaDefender Endpoint (via the “About” section or device logs).

![](https://uploads.developerhub.io/prod/2x2P/bjp7ft3v27vqwi9oil3b66317y73s4rrdtyhpvb3ey6qs2isvdp95mqualwwcxgq.png)

![](https://uploads.developerhub.io/prod/2x2P/ppaibyo4yof4u0fr5loc0gkc6lpdpn875ssla2wujnfcysi7prmym8qtmj8atwoa.png)

3. **Confirm Detection:** - Once upgraded, MetaDefender Endpoint will be able to detect MetaDefender Core properly.

## Additional Notes

- If you encounter issues during the upgrade, please collect the logs from the affected devices and share them with OPSWAT Support for further assistance.
- **Recommended Action:** Upgrade all affected devices to the latest MetaDefender Endpoint release to ensure compatibility and full detection of MetaDefender Core.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
