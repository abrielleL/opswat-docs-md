<!-- source: https://www.opswat.com/docs/macloud-sdp/release-notes/release-notes -->

# Release Notes

## [Release Date: March 26, 2025](/docs/macloud-sdp/release-notes/release-notes#release-date-march-26-2025)

Console Version: 3.53.0

**Additions in this release**

1. Added support log for IdP MFA
2. Added new OAuth Device Detail API to retrieve Public IP
3. Product Rebranding
4. Enhancement & bug fixes.

More details:

**Added support log for IdP MFA**

In this feature update, during the authentication process, once users successfully complete the authentication step, a device posture check is performed using OPSWAT IdP MFA. This ensures that the device meets security compliance requirements before access is granted. The entire activity is logged, allowing administrators to track who is using the service and monitor device compliance. This enhances security visibility and prevents unauthorized or non-compliant device access.

**Public IP added to get Device detail APIs**

The "Get Device" Detail APIs (Application Programming Interfaces) now include Public IP (Internet Protocol Address) information, improving network visibility and security monitoring. This update helps administrators track devices, detect unusual access patterns, and integrate data with security tools like Splunk. It also supports compliance auditing by providing better oversight of device activity. With this enhancement, IT teams can strengthen security, improve threat detection, and optimize network management.

**Product Rebranding**

We are pleased to unveil My OPSWAT Central Management, the enhanced and rebranded version of MetaDefender IT Access. More detail [here](https://www.opswat.com/docs/macloud-sdp/release-notes/product-rebranding)
