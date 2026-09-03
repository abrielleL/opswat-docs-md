<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/freeradius-configuration-customization -->

# FreeRADIUS Configuration Customization

> **Warning**
>
> Custom FreeRADIUS configuration packages are created, uploaded, and maintained entirely by the administrator. By uploading a custom package, you accept full responsibility for its content and for any errors, service disruptions, authentication failures, security exposures, or other issues that result from it.

> **Info**
>
> OPSWAT and MetaDefender NAC provide the mechanism to upload  a package, but do not validate, author, endorse, or guarantee the correctness of customer-supplied configuration. Use of this feature is at your own risk.

---

## 1. Overview

FreeRADIUS is the RADIUS engine that powers authentication, authorization, and accounting (AAA) in MetaDefender NAC. The NAC admin console exposes the most common RADIUS settings, but FreeRADIUS itself supports many advanced AAA scenarios that are not surfaced in the UI.

The FreeRADIUS Configuration Customization feature lets an administrator upload custom FreeRADIUS configuration files directly from the NAC admin console. This makes it possible to support advanced or non-standard AAA use cases without direct server access, and — unlike manual edits on the server — the customizations are managed by NAC so they are not silently lost when the configuration is regenerated.

### What you can do

- Upload custom FreeRADIUS configuration through the admin console.
- Upload only the specific files you need to change, instead of replacing the entire FreeRADIUS template.
- Rely on NAC to validate the uploaded content before it is applied to FreeRADIUS.
- Review who changed the configuration, and when, through the Admin event log.

### Who should use this feature

This feature is intended for NAC administrators who are **familiar** with FreeRADIUS configuration syntax and their organization's AAA requirements. Incorrect configuration can disrupt authentication for the entire network, so changes should be planned, tested, and reviewed.

---

## 2. Before You Begin

### Prerequisites

- **Administrator access** to the MetaDefender NAC admin console with permission to manage RADIUS configuration.
- **FreeRADIUS knowledge.** You should understand the FreeRADIUS files you intend to change and the effect they will have on authentication.
- **A prepared customization package.** The custom configuration file(s) you want to upload, packaged as described in Section 3.
- **A maintenance window.** Apply changes when a brief RADIUS reload will have the least impact and have a rollback plan ready.

> **Warning**
>
> **Important**: A faulty RADIUS configuration can prevent devices and users from authenticating across the network. Always validate changes in a test or staging environment first and keep a copy of the last known-good configuration.

> **Info**
>
> The customized FreeRADIUS package is your own content. You are solely responsible for it, and for any error, outage, authentication failure, misconfiguration, data exposure, or security issue that arises from uploading or applying it.

---

## 3. Preparing Your Customization

You can provide either individual customized files or a package (ZIP) containing several files. Uploading only the specific files you need is recommended — it keeps your change small, easy to review, and less likely to conflict with settings NAC manages automatically.

### Guidelines

- Include only the files you actually need to change. Do not include the entire FreeRADIUS template unless it is required.
- Keep the original directory structure and file names expected by FreeRADIUS so your files land in the correct location.
- Use valid FreeRADIUS syntax. NAC validates the package before applying it and will reject content that fails validation (see Section 6).
- Do not embed secrets or certificates in plain text unless necessary; use the dedicated certificate options where available.

### Packaging as a ZIP

If you are uploading more than one file, compress them into a single ZIP archive that preserves the folder layout. NAC extracts and validates the archive contents before applying them.

---

## 4. Uploading a Custom Configuration

The exact menu labels may vary slightly by build. In the NAC admin console, navigate to the RADIUS configuration area and locate the option to import or customize the FreeRADIUS configuration.

1. Log in to the MetaDefender NAC admin console with an administrator account.
2. Open **RADIUS Configuration** (under the authentication / network settings area).
3. Select the **Import Customized Configuration** (custom FreeRADIUS) option.
4. Choose the specific **ZIP** package.
5. Review the file list shown by NAC to confirm the correct files were selected.
6. **Save** the configuration. NAC validates the uploaded content at this point.
7. Click **Apply & Use** (or Apply) to activate the configuration on the RADIUS server.

> **Info**
>
> Tip: If validation fails, the configuration is not applied. Correct the reported issue in your files and upload again. Your previously active configuration remains in effect until a valid change is applied.

---

## 5. Verifying and Testing

After applying a custom configuration, confirm that authentication continues to work as expected before ending your maintenance window.

1. Confirm the apply operation completed without errors in the admin console.
2. Perform a test authentication (for example, a test device or user) that exercises the behavior you customized.
3. Check that authenticated sessions appear correctly on the **Session** page.
4. Review server/RADIUS logs for warnings or rejected requests related to your change.
5. Verify the change was recorded in the Admin event log (see Section 7).

---

## 6. Audit Logging

Every custom FreeRADIUS configuration action is recorded in the Admin event log so administrators can audit who made a change and when. This includes uploading a custom FreeRADIUS configuration and customizing the FreeRADIUS certificate.

1. Open the **Admin Event Log** area of the console.
2. Locate the entry corresponding to your configuration upload or certificate change.
3. Confirm the actor, timestamp, and action match the change you made.
