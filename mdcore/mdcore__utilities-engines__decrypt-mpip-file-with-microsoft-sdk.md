<!-- source: https://www.opswat.com/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk -->

# Decrypt Microsoft Purview Information Protection (MPIP) files

## [Overview](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#overview)

Microsoft Purview Information Protection (MPIP, previously Microsoft Information Protection / MSIP and Azure Information Protection / AIP) lets organizations apply sensitivity labels to files. When a label carries an **encryption** setting, the file is wrapped with Azure Rights Management (Azure RMS) protection: the content is AES-encrypted, and the key needed to open it is held by the Azure RMS service for the tenant that applied the label. Only identities that RMS authorizes can obtain that key.

MetaDefender Core has detected these files, the File Type engine reports them as `MSO-ENCRYPTED-MSIP` (Office documents), but could not look inside them, so the payload was treated as opaque and could only be allowed or blocked by policy.

Starting with Archive Extraction engine 8.1.0, the Archive Extraction module can decrypt MPIP-protected files in place and hand the original data to the rest of the workflow (Multiscanning, Deep CDR, Proactive DLP, Sandbox, and so on). Decryption uses the Microsoft Information Protection (MIP) File SDK and a service principal that your Microsoft 365 tenant administrator authorizes as an Azure RMS *super user*.

> **Scope:** the integration decrypts files protected by **your own tenant** only. Azure RMS scopes super-user rights per tenant by design; files labeled by a partner or customer tenant cannot be opened with your credentials. Multi-tenant organizations must repeat the tenant setup for each tenant and configure a MetaDefender Core instance per tenant.

---

## [How MPIP protection and decryption work](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#how-mpip-protection-and-decryption-work)

### [The decryption handshake](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#the-decryption-handshake)

When the Archive Extraction module receives an `MSO-ENCRYPTED-MSIP` file with MPIP decryption enabled, the built-in MIP service performs the following sequence. Steps 1–3 happen once at startup and are cached; steps 4–6 run per file.

| Step | Action |
| --- | --- |
| 1 | Authenticate as the service principal (client-credentials flow with Tenant ID, Client ID, Client Secret) |
| 2 | Acquire a token for the policy sync service and download the tenant's sensitivity-label policy |
| 3 | Acquire a token for Azure RMS |
| 4 | Parse the file, extract the publishing license |
| 5 | Send the publishing license to RMS and request an **end-user (use) license**. RMS checks the token's object ID against the tenant's super-user group and, if it matches, returns the unwrapped content key. |
| 6 | Decrypt the payload locally with the content key and pass the plaintext file to the workflow as an extracted child |

**Security boundary:** the document body never leaves the MetaDefender Core host. RMS sees only the publishing license, the content ID, and the authentication token. This is relevant for data-residency and compliance conversations — the integration does not upload customer content to Microsoft.

### [Why a super user](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#why-a-super-user)

A normal user can only open files whose publishing license grants them rights. A security gateway must open *every* file regardless of who it was addressed to. Azure RMS provides the **super-user** feature for exactly this case: members of the designated super-user group are always granted full use licenses for any content protected by the tenant. The MetaDefender Core service principal is added to that group. Removing it from the group is an instant kill-switch, no change is required on the MetaDefender Core side.

### [Performance characteristics](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#performance-characteristics)

| Metric | Typical value |
| --- | --- |
| First decryption after engine start | ~3–5 s (token acquisition, policy sync, first RMS round trip) |
| Subsequent files | ~200–800 ms each (only the use-license request hits the network) |
| Token lifetime | ~1 hour, refreshed automatically |
| Policy cache | Persisted on disk, refreshed when label policy changes |
| Practical concurrency | ~8 parallel RMS requests before service-side rate limiting |

---

## [Prerequisites](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#prerequisites)

### [On the Microsoft 365 side](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#on-the-microsoft-365-side)

- Global Administrator or Compliance Administrator role on the tenant that protects the files.
- Windows PowerShell 5.1.
- Access to the [Microsoft Entra admin center](https://entra.microsoft.com).
- Azure Rights Management activated on the tenant (it is on by default for most Microsoft 365 subscriptions that include Purview Information Protection).

### [On the MetaDefender Core side](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#on-the-metadefender-core-side)

- MetaDefender Core with Archive Extraction engine **8.1.0 or later**.

- Outbound HTTPS (443) from the MetaDefender Core server to:

  - `login.microsoftonline.com` and `login.windows.net`
  - `api.aadrm.com` and `*.aadrm.com`
  - `syncservice.o365syncservice.com`

---

## [Part 1 — Set up the Microsoft 365 tenant](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#part-1--set-up-the-microsoft-365-tenant)

Programmatic decryption requires **all four** of the following to be true. Skipping any one of them produces an `AccessDenied` error at scan time that does not say which condition failed, so verify each before troubleshooting MetaDefender Core.

1. An Entra ID application with the right API permissions
2. The Azure RMS super-user feature enabled on the tenant
3. A super-user group designated in RMS
4. The application's service principal added as a member of that group

### [Step 1 — Register the Entra ID application](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-1--register-the-entra-id-application)

1. Sign in to the **Entra admin center** → **Identity** → **App registrations** → **New registration**.
2. Fill in:

   - **Name:** `MetaDefender-MPIP-Decryptor`
   - **Supported account types:** Accounts in this organizational directory only (single tenant)
   - **Redirect URI:** leave blank
3. Click **Register**.
4. From the **Overview** page, record the **Application (client) ID** and **Directory (tenant) ID**. You will enter both in MetaDefender Core.

#### [Step 1a — Create a client secret](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-1a--create-a-client-secret)

1. In the registered app → **Certificates & secrets** → **Client secrets** → **New client secret**.
2. Description: `metadefender-core`; expiry: 24 months (the maximum).
3. Click **Add**, then immediately copy the **Value** column (not the Secret ID).

### [Step 2 — Grant API permissions](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-2--grant-api-permissions)

In the app registration → **API permissions** → **Add a permission**.

#### [2a. Azure Rights Management Services](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#2a-azure-rights-management-services)

1. Open the **APIs my organization uses** tab and search for `Azure Rights Management Services`.
2. Choose **Application permissions**.
3. Add `Content.SuperUser` and `Content.Writer`.

> If `Azure Rights Management Services` does not appear in the search, the RMS service principal has not been provisioned in your tenant. Run the following in Windows PowerShell, wait 5–10 minutes, and retry:
>
> Install-Module -Name AIPService -Force
> Connect-AipService
> Enable-AipService

#### [2b. Microsoft Information Protection Sync Service](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#2b-microsoft-information-protection-sync-service)

This API is hidden from the default picker. Use one of these methods.

**Method A — search by application ID.** In **APIs my organization uses**, paste this GUID into the search box:

870c4f2e-85b6-4d43-bdda-6ed9a579b725

Select the **Microsoft Information Protection Sync Service** tile → **Application permissions** → add `UnifiedPolicy.Tenant.Read.All`.

**Method B — edit the manifest (more reliable).** App registration → **Manifest** → add this object to the `requiredResourceAccess` array, then save:

{
"resourceAppId": "870c4f2e-85b6-4d43-bdda-6ed9a579b725",
"resourceAccess": [
{
"id": "23e15f4a-67fa-4f72-b1da-219ce72be8d0",
"type": "Role"
}
]
}
#### [2c. Grant admin consent](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#2c-grant-admin-consent)

On the **API permissions** page click **Grant admin consent for [tenant]**. All three permissions must show **Granted**:

| API | Permission | Type |
| --- | --- | --- |
| Azure Rights Management Services | `Content.SuperUser` | Application |
| Azure Rights Management Services | `Content.Writer` | Application |
| Microsoft Information Protection Sync Service | `UnifiedPolicy.Tenant.Read.All` | Application |

### [Step 3 — Create the super-user group](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-3--create-the-super-user-group)

1. **Entra admin center** → **Identity** → **Groups** → **All groups** → **New group**.
2. Fill in:

   - **Group type:** Microsoft 365
   - **Group name:** `mpip-superusers`
   - **Group email address:** `mpip-superusers` (the tenant domain is appended automatically)
   - **Owner:** your admin account
   - **Members:** leave empty for now
3. Click **Create** and wait about a minute for provisioning. Note the group's full email address from its Overview page.

### [Step 4 — Enable the RMS super-user feature](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-4--enable-the-rms-super-user-feature)

In **Windows PowerShell 5.1** or **Azure Cloud Shell (PowerShell)**:

# One-time per machine
Install-Module -Name AIPService -Force
# Browser sign-in as Global Admin or Compliance Admin
Connect-AipService
# Turn on the super-user feature for the tenant
Enable-AipServiceSuperUserFeature
# Designate the group from Step 3
Set-AipServiceSuperUserGroup -GroupEmailAddress "mpip-superusers@yourtenant.onmicrosoft.com"

Replace `yourtenant.onmicrosoft.com` with your tenant's primary domain.

### [Step 5 — Add the service principal to the super-user group](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-5--add-the-service-principal-to-the-super-user-group)

1. **Entra admin center** → **Identity** → **Groups** → open `mpip-superusers`.
2. **Members** → **Add members**.
3. Search for `MetaDefender-MPIP-Decryptor`. The service principal shows a gear icon rather than a person icon. Select it → **Select** → **Add**.

If the service principal does not appear, force its creation and retry:

Connect-MgGraph -Scopes "Application.ReadWrite.All"
New-MgServicePrincipal -AppId "<client-id-from-step-1>"
### [Step 6 — Verify the tenant configuration](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-6--verify-the-tenant-configuration)

Get-AipServiceSuperUserFeature
# Expected: Enabled
Get-AipServiceSuperUserGroup
# Expected: mpip-superusers@yourtenant.onmicrosoft.com

If either result is `Disabled` or empty, re-run the corresponding cmdlet from Step 4.

### [Step 7 — Hand off credentials](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#step-7--hand-off-credentials)

The person configuring MetaDefender Core needs:

| Value | Where to find it |
| --- | --- |
| Tenant ID | App registration → Overview → Directory (tenant) ID |
| Client ID | App registration → Overview → Application (client) ID |
| Client secret | The value copied in Step 1a |

---

## [Part 2 — Configure MetaDefender Core](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#part-2--configure-metadefender-core)

### [Enable MPIP decryption in the Archive Extraction module](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#enable-mpip-decryption-in-the-archive-extraction-module)

1. In the MetaDefender Core Management Console go to **Inventory → Modules → Utilities → Archive Extraction** and open its settings.
2. Enable **Decrypt MSIP-protected documents**. The option is disabled by default.
3. Enter the values from Step 7:

   - **Tenant ID**
   - **Client ID**
   - **Client Secret**
4. Save. The Archive Extraction engine restarts and launches its MIP processing service. The service authenticates to the tenant and downloads the label policy at startup, so the first scan after enabling the feature takes a few seconds longer.

### [Workflow configuration](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#workflow-configuration)

MPIP-protected files are handled as an archive-like container: the decrypted document becomes the single extracted child of the original file and flows through every engine enabled in the workflow.

Files whose decryption fails (wrong tenant, service principal not authorized, network error) are reported the same way as failed Office or PDF password decryption: the file remains detected as `MSO-ENCRYPTED-MSIP` / `PDF-ENCRYPTED-MSIP` with an extraction failure, and the workflow's existing handling for encrypted archives applies.

### [Verify](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#verify)

1. Using Microsoft Word signed in to the configured tenant, create a document and apply a sensitivity label whose settings include **Encrypt files**. Save it.
2. Submit the file to MetaDefender Core (Management Console → Process, or the REST API).
3. In the scan result:

   - The top-level file is detected as `MSO-ENCRYPTED-MSIP`.
   - **Extracted files** shows one child — the decrypted document, detected as the ordinary Office type (for example `Microsoft Word Document`).

### [Troubleshooting](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#troubleshooting)

| Symptom | Likely cause | Fix |
| --- | --- | --- |
| `AccessDenied` on every file, tenant setup just completed | Super-user group membership has not propagated to RMS | Wait up to 30 minutes and retry. Confirm with `Get-AipServiceSuperUserGroup`. |
| `AccessDenied` persists after 30 minutes | Service principal not in the super-user group, or super-user feature disabled | Re-check Steps 4–6. Ensure the group is a **Microsoft 365** group, not a security group. |
| `The protection service is unavailable` / HTTP 503 from `api.aadrm.com/my/v2/enduserlicenses` | Azure RMS not activated on the *issuing* tenant, or credentials belong to a different tenant than the one that protected the file | Run `Get-AipServiceConfiguration` on the issuing tenant; `FunctionalState` must be `Enabled`. Confirm the Tenant ID in MetaDefender Core matches the tenant that applied the label. |
| Token acquired but only for `syncservice.o365syncservice.com`; RMS call fails | `Azure Rights Management Services` permissions missing or admin consent not granted | Re-check Step 2a and 2c. All three permissions must show **Granted**. |
| Feature stopped working after months of operation | Client secret expired | Create a new secret (Step 1a), update MetaDefender Core, delete the old one. |

---

## [Limitations](/docs/mdcore/utilities-engines/decrypt-mpip-file-with-microsoft-sdk#limitations)

- **Same-tenant only.** Files protected by other tenants cannot be decrypted.
- **Decryption only.** MetaDefender Core does not re-apply the label or encryption to the sanitized or extracted output.
- **Office and PDF payloads.** Supported inputs are the `MSO-ENCRYPTED-MSIP` file types.

---
