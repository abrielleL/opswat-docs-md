<!-- source: https://www.opswat.com/docs/filescan/integrations/misp -->

# MISP

The MISP is an open source software solution for collecting, storing, distributing and sharing cyber security indicators and threats about cyber security incidents analysis and malware analysis. You can find more information about MISP [here](https://www.misp-project.org).

Note

To integrate with MISP, it is necessary to have a pre-installed MISP instance.

## [Integrating MetaDefender Sandbox with MISP](/docs/filescan/integrations/misp#integrating-metadefender-sandbox-with-misp)

To create an integration, navigate to the **Admin Panel**.

Select "Settings" from the menu bar, and you'll find the MISP tab under Configuration.

Enter your MISP API key and MISP API URL, check the "*MISP_ENABLED*" checkbox, and then save the settings.

### [Configuration options](/docs/filescan/integrations/misp#configuration-options)

| Field | Description |
| --- | --- |
| `MISP_API_KEY` | MISP server API-key |
| `MISP_API_URL` | The address of the MISP server |
| `MISP_TIMEOUT` | Timeout, value in seconds. The 0 value disables timeout check! |
| `MISP_ENABLED` | Check-box to enable or disable MISP integration |

Note

note that in order for Sandbox results to be added as events to MISP, the url format should be:

**<MISP URL>/events/add**

If everything is correct, click on the "Save" button.

If MISP integration is enabled, then **Confirmed Threat** and **High Risk** results will be published.

If all settings are correct, events will appear in the MISP instance. For example:

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
