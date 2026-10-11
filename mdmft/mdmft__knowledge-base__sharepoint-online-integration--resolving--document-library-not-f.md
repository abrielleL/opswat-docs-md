<!-- source: https://www.opswat.com/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f -->

# SharePoint Online integration: resolving "document library not found" and "Access denied" errors

Summarize Page    Connect to Cursor Connect to VS Code

**Applies to:** MetaDefender Managed File Transfer — SPO (SharePoint Online) storage integration

**Related:** MetaDefender Storage Security™ (for comparison; see Notes)

Before troubleshooting document library or permission errors, confirm the integration's Environment Type matches your tenant, Azure Commercial or Azure Government. Picking the wrong type causes the connection test to fail earlier, before the integration ever reaches the document library check.

## [**Summary**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#summary)

When configuring a SharePoint Online integration in MetaDefender Managed File Transfer, the connection test can fail in two distinct, unrelated ways:

- The document library is reported as not found, even though it exists

- The credentials connect, but the test fails with "Access denied" while creating the integration's metadata column

This article covers a prerequisite check (the Environment Type selector) and then explains both causes and how to resolve them. The most commonly missed item is the **Sites.Manage.All** application permission, which is required for the metadata-column step and is not covered by the usual read/write permissions.

## [**Prerequisite — confirm the Environment Type**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#prerequisite--confirm-the-environment-type)

The SharePoint Online integration setup includes an **Environment Type** selector with two options:

- **Azure Commercial** (Commercial / GCC)

- **Azure Government** (GCC High / DoD)

These point to two completely separate Microsoft cloud environments, each with its own sign-in and Microsoft Graph endpoints: the commercial cloud uses [login.microsoftonline.com](http://login.microsoftonline.com) and [graph.microsoft.com](http://graph.microsoft.com), while the U.S. Government cloud uses [login.microsoftonline.us](http://login.microsoftonline.us) with [graph.microsoft.us](http://graph.microsoft.us) for GCC High tenants or [dod-graph.microsoft.us](http://dod-graph.microsoft.us) for DoD (Department of Defense) tenants. GCC (Government Community Cloud) tenants run on the commercial endpoints, which is why the selector groups them under Azure Commercial.

Before troubleshooting document library or permission errors, confirm the integration's Environment Type matches your tenant — Azure Commercial or Azure Government. Selecting the wrong type causes the connection test to fail earlier, before the integration ever reaches the document library check, typically with a general connection or authentication error rather than the messages covered in this article.

## [**Symptoms**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#symptoms)

One or more of the following appears during the SharePoint Online connection test. (If the test instead fails with a general connection or authentication error before either message appears, check the Environment Type first — see the prerequisite above.)

Document library not found:

> Document library 'Documents' not found in https://<tenant>.sharepoint.com/sites/<site> 
> Document library 'Shared%20Documents' not found in https://<tenant>.sharepoint.com/sites/<site>

Access denied while creating the metadata column:

> Pull - Test Failed 
> These credentials do not have permission to pull files. Please double-check if 
> your credential includes: Sites.Read.All. 
> Error: Error creating MFT metadata column: Access denied

## [**Cause**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#cause)

### [**1. "Document library not found"**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#step-2--grant-the-required-microsoft-graph-permissions)

The SharePoint Online integration matches the document library by its **display name** — the title shown in the SharePoint web interface — not by its internal/URL name. The display name is localized to the site's language, and the value is matched literally (it is not URL-decoded). As a result:

- On a non-English site, the default library's display name is the localized term (for example, "Dokumenty" on a Polish-language site), so entering "Documents" fails

- Entering the internal/URL form "Shared%20Documents" fails, because the integration searches for a library whose title literally contains "%20" rather than a space

### [**2. "Access denied" while creating the metadata column**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#step-3--verify-the-configuration)

To track transfers, the integration creates a metadata column in the target library. Creating a column changes the library's **structure** (its schema); it is not a change to the library's content.

Application permissions such as Sites.ReadWrite.All and Files.ReadWrite.All grant read and write access to **items and files**, but they do not grant permission to modify a library's structure. Creating a column therefore fails with "Access denied" even when those content permissions are present, correctly set to Application type, and admin-consented. A management-level permission — **Sites.Manage.All** — is required for this step.

The error hint that suggests "[Sites.Read](http://Sites.Read).All" is misleading. The operation that fails is a write (creating a column), not a read, so adding read permission does not resolve it.

## [**Resolution**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#1-document-library-not-found)

### [**Step 1 — Enter the document library name correctly**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#background)

Enter the library's display name exactly as it appears in SharePoint for that specific site, in **plain text** (not URL-encoded):

- Use the localized title shown in the SharePoint interface — for example, "Dokumenty" on a Polish-language site

- Enter spaces as literal spaces, never as "%20"

- For names containing accented or special characters, type them exactly as displayed

The most reliable method is to copy the name directly from **Site Contents** on the site, or from the name field returned by the Microsoft Graph /sites/{site-id}/drives endpoint. The match is exact, so a stray space, casing difference, or hidden character is reported as not found.

### [**Step 2 — Grant the required Microsoft Graph permissions**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#display-name-vs-internal-name-and-localization)

On the Microsoft Entra (formerly Azure AD) app registration used by the integration, grant the following application permissions, then grant admin consent:

| **Permission** | **Type** | **Purpose** |
| --- | --- | --- |
| Files.ReadWrite.All | Application | Pull and push files |
| Sites.ReadWrite.All | Application | Read and write list items and file metadata |
| Sites.Manage.All | Application | Create the integration's metadata column (a list-schema change) — required |

Notes on the permissions:

- Sites.FullControl.All may be used in place of Sites.Manage.All, as it includes it, but Sites.Manage.All is sufficient and follows the principle of least privilege

- Sites.Read.All and Group.ReadWrite.All are not required for this integration step

- The integration authenticates app-only (client ID and client secret), so the permissions must be **Application** type — Delegated permissions of the same name are not used

### [**Step 3 — Verify the configuration**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#content-permissions-vs-management-permissions)

Before re-testing, confirm:

- The integration's **Environment Type** matches your tenant's cloud — Azure Commercial or Azure Government (see the prerequisite above)

- Each permission's **Type** column shows "Application," not "Delegated"

- Admin consent is granted (the status shows "Granted for <tenant>")

- The permissions are on the **same** app registration whose client ID is configured in the integration

Then re-run the connection test with the document library set to its correct display name. The metadata column is created and the test passes.

## [**Background**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#2-access-denied-while-creating-the-metadata-column)

### [**Display name vs. internal name, and localization**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#notes)

Every SharePoint document library has two names:

- An internal/URL name that is fixed at creation and never translated — for the default library this is always "Shared Documents" (shown in the URL as /Shared Documents/)

- A display name (title) that the SharePoint multilingual interface presents in the site's language — "Documents" in English, "Dokumenty" in Polish, and so on

The SharePoint Online integration in MetaDefender Managed File Transfer matches on the **display name**, which is why the correct value depends on the site's language and must be entered as plain text.

### [**Content permissions vs. management permissions**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#references)

Microsoft Graph separates permission to change **content** from permission to change **structure**:

- Sites.ReadWrite.All and Files.ReadWrite.All — add, edit, and remove items and files

- Sites.Manage.All — create and manage lists, columns, and content types

- Sites.FullControl.All — full control, including permissions

Creating a column is a structural (schema) change, so it requires Sites.Manage.All even when the integration already has read/write access to content.

## [**Notes**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#resolution)

**Comparison with MetaDefender Storage Security.** The equivalent storage integration in MetaDefender Storage Security resolves the library by its internal/URL name (for example, Shared%20Documents) and then displays the localized title for reference. It is therefore unaffected by the display-name behavior described above, and this difference between the two products is expected.

Always confirm the exact, current permission requirements against the official MetaDefender Managed File Transfer SharePoint Online integration documentation, as requirements can change between releases.

## [**References**](/docs/mdmft/knowledge-base/sharepoint-online-integration--resolving--document-library-not-f#step-1--enter-the-document-library-name-correctly)

- Microsoft Graph permissions reference — <https://learn.microsoft.com/en-us/graph/permissions-reference>

- Microsoft Graph national cloud deployments (endpoint differences between Azure Commercial and Azure Government) — <https://learn.microsoft.com/en-us/graph/deployments>

- Microsoft Graph documentation on creating list columns (column creation requires Sites.Manage.All)

- MetaDefender Managed File Transfer — SharePoint Online integration documentation (OPSWAT product documentation)
