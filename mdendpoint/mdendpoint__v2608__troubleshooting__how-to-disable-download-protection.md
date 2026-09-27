<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/troubleshooting/how-to-disable-download-protection -->

# How to Disable Download Protection

> **Check Your Version:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows.

Download Protection is controlled by the **Secure Downloads** setting in the endpoint policy. When Secure Downloads is disabled, the **Download Protection** section will no longer appear in the sidebar.

## Steps

1. Go to [Home - My OPSWAT](https://my.opswat.com/portal/home)  and log in.
2. Click **Central Management**.
3. Navigate to **Policies → Endpoint Security**.

![](https://uploads.developerhub.io/prod/2x2P/p0hkp8uzcng5aexgvc08fw2yxpa5q0rz96rq5owjdeihhnol635se5iu7634sw90.png)

4. Open the policy that is assigned to the affected endpoint:
   - If it uses the **Default Policy**, open that policy.
   - Otherwise, open the custom policy assigned to the endpoint.
5. Go to **Advanced Endpoint Protection → Enable Threat Detection for Windows**.
6. Locate **Secure Downloads** and make sure it is **disabled (unticked)**.

![](https://uploads.developerhub.io/prod/2x2P/9ptxumduz1jq3rlf7dc0c4lyvymctz20pl6vgtcfzq552yztl0auvae9ym408ey7.png)

7. Save the policy and allow it to sync to the endpoint.

## Verification

After the policy is applied:

- The **Download Protection** section should disappear from the sidebar.
- No service restart is required, but the policy must finish syncing.

## Troubleshooting

If the section still appears:

- Confirm the endpoint is assigned to the policy you modified.
- Double-check that **Secure Downloads** is disabled in that policy.
- Trigger a manual policy refresh on the endpoint if needed.

> **Support:**
>
> If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
