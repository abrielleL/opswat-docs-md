<!-- source: https://www.opswat.com/docs/netwalldiode/v1.14.0/knowledge-base/aveva-pi-connector---what-are-the-possible-values-for-some-ha-ta -->

# AVEVA PI Connector - What are the possible values for some HA tags and what do they mean in MetaDefender Optical Diode?

**Check Your Version:**

This article applies to MetaDefender Optical Diode supported version configured on **High Availability** mode utilizing **AVEVA Pi connector.**

| **Tag Name** | **Description** | **Values** |
| --- | --- | --- |
| FlankerStatus | This tag contains the current status of the flanker connection to the PI database.  If the flanker is connected to PI, the status will show as “**Connected**.”  If the flanker is not connected to PI, the status will show as “**Not Connected**.”  However, since the ”Not Connected” status obviously cannot be written to PI, it will only show in Syslog | - Connected - Not Connected |
| SelectedFlanker | This tag contains the online/offline status of the flanker that is reporting.  If the Flanker is online, then it is acting as the primary flanker.  If the Flanker is offline, then it is acting as secondary. | - Online - Offline |
| SelectedHa | This tag contains the status of each of the HA pair. ”Online” acting as primary. “Standby” acting as secondary. | - Online - Standby |
| HaStatusA/B | This tag provide health status information of the HA pair. | - OK - Bad |

**Support:**

If **Further Assistance** is required or you have any other questions, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

MetaDefender
