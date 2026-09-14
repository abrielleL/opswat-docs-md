<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration -->

# MetaDefender Industrial Firewall (MDIF) Integration

# [MetaDefender Industrial Firewall (MDIF) Integration](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#metadefender-industrial-firewall-mdif-integration)

Starting in version 4.8.5, MetaDefender Kiosk can recognize a connected MetaDefender Industrial Firewall (MDIF) device automatically and host its setup and configuration screen directly inside the Kiosk interface — instead of treating it as a removable-media device to be scanned. This lets an operator plug in an MDIF unit at the Kiosk and complete the device's own setup flow (for example, authenticating, generating a report, or emailing it to a reviewer) without leaving the Kiosk screen.

## [Prerequisites](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#prerequisites)

- MetaDefender Kiosk 4.8.5 or later.
- An MDIF device with valid OPSWAT-issued device credentials. Kiosk verifies the device automatically; no manual device registration is required by the administrator.
- Administrator access to the Kiosk Management Console, or to Central Management if the Kiosk is centrally managed.
- A physical connection Kiosk can detect (for MDIF, this is typically a direct cable connection that Kiosk recognizes as an attached device).

## [Setting Up an Integration Workflow](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#setting-up-an-integration-workflow)

1. Sign in to the Kiosk Management Console as an administrator and navigate to the **Workflows** page.
2. Create a new workflow and choose the **Integration Workflow** type.
3. Fill in the standard workflow settings — name, membership (which users/groups this workflow applies to), any operator questions, report settings, and email settings — the same way you would for any other Kiosk workflow.
4. On the workflow's **Processing** tab, configure the options specific to the connected product (MDIF or MetaDefender Drive). These options are supplied by the product itself, so the exact fields you see depend on which product the workflow is for.
5. Make sure the **Integration Workflow** group is turned on. Both MDIF and MetaDefender Drive workflows are controlled by this single group toggle — turning it off disables device recognition for both products at once.

Note

If your Kiosk is enrolled in Central Management, create and edit Integration Workflows from Central Management rather than locally on the Kiosk. Central Management is the source of truth for an enrolled Kiosk's workflows, and a workflow created only on the Kiosk itself may be removed the next time policy syncs from Central Management.

## [How Device Recognition Works](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#how-device-recognition-works)

When a device is connected, Kiosk checks whether it is a recognized MDIF or MetaDefender Drive unit before deciding how to handle it:

- If the device is recognized and its Integration Workflow is enabled, Kiosk hands control to that product's own setup screen, shown inside the Kiosk window with the on-screen keyboard available automatically.
- If the device cannot be verified, or its Integration Workflow is turned off, Kiosk falls back to treating it as ordinary removable media.

This check happens automatically — administrators don't need to configure device identities or serial numbers manually.

## [Email and Reporting](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#email-and-reporting)

If the connected product's workflow includes email, the product's own interface composes and requests that email be sent once its setup flow finishes — for example, sending a generated report to a reviewer. Kiosk delivers the email using your existing email configuration (sender, SMTP/Graph settings, and Active Directory-based recipient lookup if you've enabled it for the workflow).

If the product generates a report or document that needs to carry the Kiosk operator's digital signature, Kiosk signs it automatically using the certificate configured for that workflow's report settings — the product does not need, and cannot supply, its own signing certificate.

Note

Not every placeholder value available in other Kiosk workflows (like scan results) is available to an Integration Workflow, since these workflows don't run a media scan. Values tied to the connected device and the current user (such as username or device model) are available; values that depend on a completed file scan are not.

## [Upgrading from an Earlier Version](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#upgrading-from-an-earlier-version)

If you're upgrading a Kiosk that already had MetaDefender Drive configured, your existing MD Drive settings are carried forward automatically into the new Integration Workflow format — you don't need to reconfigure MD Drive after upgrading to 4.8.5. Your Integration Workflow configuration is also included in Kiosk's configuration backup and restore, the same as any other workflow.

---

## [Related Links](/docs/mdkiosk/v4.8.5/advanced-deployment/metadefender-industrial-firewall--mdif--integration#related-links)

- [Configuring with MetaDefender Drive](/docs/mdkiosk/v4.8.5/configuration/configuring-with-metadefender-drive)
- [Kiosk Workflows](/docs/mdkiosk/v4.8.5/operating/kiosk-workflows)
- [Workflows Page](/docs/mdkiosk/v4.8.5/operating/workflows-page)
- [Ivanti Device Control Encrypted Device Integration](/docs/mdkiosk/v4.8.5/advanced-deployment/ivanti-device-control-encrypted-device-integration)
