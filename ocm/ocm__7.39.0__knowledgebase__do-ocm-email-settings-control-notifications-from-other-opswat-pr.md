<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/do-ocm-email-settings-control-notifications-from-other-opswat-pr -->

# Do OCM Email Settings Control Notifications from Other OPSWAT Products?

This article applies to all OPSWAT Central Management V7.5.0+ releases deployed on Windows or Linux systems.

In **OCM v7**, configuring the mail (SMTP) server applies **only to OCM**. It does not control, forward, or centralize notifications from other products such as Core, ICAP,or any additional modules in your environment.

Each product is responsible for its own **independent email configuration** and notification behavior. If you want to receive alerts from Core, ICAP, or others, you must **manually configure SMTP settings** within each product.

### [**How Email Notifications Work**](/docs/ocm/7.39.0/knowledgebase/do-ocm-email-settings-control-notifications-from-other-opswat-pr#how-email-notifications-work)

- **OCM** sends alerts only for its own events and operations.
- Core, ICAP, and other modules send their own notifications **independently**.
- There is **no shared or centralized** email system between OCM and other products.

### [**Exception: MetaDefender Kiosk Windows**](/docs/ocm/7.39.0/knowledgebase/do-ocm-email-settings-control-notifications-from-other-opswat-pr#exception-metadefender-kiosk-windows)

OCM provides deeper integration with **MetaDefender Kiosk Windows**, allowing limited centralized reporting and email capabilitie. For more information, you can refer to this support article: [MetaDefender Kiosk Windows Dashboard](https://www.opswat.com/docs/ocm/integrations/metadefender-kiosk-dashboard#overview-tab)

### [**SMTP Server Exceptions**](/docs/ocm/7.39.0/knowledgebase/do-ocm-email-settings-control-notifications-from-other-opswat-pr#smtp-server-exceptions)

If your SMTP server uses restrictions (e.g., firewalls, filters, or whitelisting), make sure to grant **separate access for each product**. Since they send emails individually, a rule for OCM alone will **not** cover Core, ICAP, or others.

### [**Summary**](/docs/ocm/7.39.0/knowledgebase/do-ocm-email-settings-control-notifications-from-other-opswat-pr#summary)

- Email settings in OCM **do not apply** to other products.
- Each product must be **configured separately** to send alerts.
- Notifications are **not routed through OCM**, except for **Kiosk reports**.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
