<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-forcefully-unenroll-a-metadefender-core-instance-from-o -->

# How do I forcefully unenroll a MetaDefender Core instance from OPSWAT Central Management (OCM)?

> **Check Your Version:**
>
> This article applies to OCM versions 7, 8, and 10

## **Issue**

Unenrolling a MetaDefender Core instance from OPSWAT Central Management (OCM) via the Web UI sometimes fails due to cached old connection states. By default, the Web UI sets the force parameter to false, which can prevent successful unenrollment.

## **Resolution**

### OCM Versions 8 and 10

To bypass the cached connection state and forcefully unenroll the Core from OCM, execute the following request from the command prompt:

```plaintext
curl -I -X DELETE "http://<core_ip>:8008/admin/ocm?force=true" \
-H "Accept: application/json, text/plain, */*" \
-H "Apikey: < >"
```

**Notes:**

- Replace `<core_ip>` with the IP address of your Core instance.
- Using `force=true` ensures the Core is unenrolled even if a cached connection state exists.
- When using `force=true`, the Core does not send an unenroll request to OCM. Instead, it only clears the OCM section locally. This means the local Core instance becomes unmanaged from OCM, while the Core instance remains visible on the OCM dashboard.

### OCM Version 7

For OCM version 7, you must use a different API endpoint. Execute the following request from the command prompt:

```plaintext
curl -I -X DELETE "http://<core_ip>:8008/admin/manage" \
-H "Accept: application/json, text/plain, */*" \
-H "Apikey: < >"
```

**Notes:**

- Replace `<core_ip>` with the IP address of your Core instance.
- This endpoint does not support query parameters (i.e., `force=true` is not available for OCM 7).
- After unenrolling via this method, the Core instance will remain displayed in the OCM 7 dashboard with a status of "Disconnected".

**Recommendation:** After forcefully unenrolling the Core (OCM 8 and 10), note that the Core instance may still remain visible on the OCM dashboard since the unenroll request is only cleared locally. Verify the unenrollment status and re-enroll if required. For OCM 7, expect the Core to show as "Disconnected" in the OCM dashboard.

> **Support:**
>
> If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
