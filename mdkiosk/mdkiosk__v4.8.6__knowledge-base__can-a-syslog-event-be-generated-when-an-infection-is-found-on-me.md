<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/can-a-syslog-event-be-generated-when-an-infection-is-found-on-me -->

# Can a Syslog event be generated when an infection is found by MetaDefender Kiosk?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdkiosk/v4.8.6/knowledge-base/can-a-syslog-event-be-generated-when-an-infection-is-found-on-me#overview)

MetaDefender Kiosk does support the generation of **Syslog events** when infected files are detected during processing. This integration enables centralized monitoring and response by forwarding security-relevant events to a designated Syslog server.

Pro Tip:

Syslog, also known as System Logging Protocol, is designed to send system log and event messages from a network of devices to a centralized syslog server for monitoring, review and remediation.

---

## [Configuration](/docs/mdkiosk/v4.8.6/knowledge-base/can-a-syslog-event-be-generated-when-an-infection-is-found-on-me#configuration)

To enable Syslog event generation in MetaDefender Kiosk:

1. Open the **Kiosk Management Console**.
2. Navigate to **Settings > Logs > Syslog.**
3. Click **Add New Server** to add a Syslog destination.
4. Enter the required server details as illustrated in the configuration interface.

Once configured, MetaDefender Kiosk will automatically log events related to file infections and other relevant actions.

Support:

If you have followed all of the steps above but are still unable to **Generate a Syslog Event When an Infection is Found by MetaDefender Kiosk**, please follow these instructions on [How To Create a Support Package](/docs/mdkiosk/v4.8.6/knowledge-base/how-do-i-create-a-support-package-for-metadefender-kiosk-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
