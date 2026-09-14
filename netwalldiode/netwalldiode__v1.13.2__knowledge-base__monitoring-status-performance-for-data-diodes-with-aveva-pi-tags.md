<!-- source: https://www.opswat.com/docs/netwalldiode/v1.13.2/knowledge-base/monitoring-status-performance-for-data-diodes-with-aveva-pi-tags -->

# Monitoring status/performance for Data Diodes with AVEVA PI tags

The status/performance of both Blue and Red zones of the Diodes can be tracked using AVEVA PI tags.

**Why**

Netwall has the ability to write its internal status/performance counters to AVEVA PI Tags. This ability exists in both security zones. In addition, since the status/performance information is in fact AVEVA PI Tags, the same mechanism used to replicate AVEVA PI Database can be used to replicate the Blue zone status/performance to the Red AVEVA PI Database, allowing the administrator in the Red zone to monitor both.

#### [How](/docs/netwalldiode/v1.13.2/knowledge-base/monitoring-status-performance-for-data-diodes-with-aveva-pi-tags#how)

The statistics, displayed by the Netwall Blue/Red security zones can be published to the corresponding AVEVA PI Database using Tags. Once the tags have been created, the status/performance of the Netwall can be monitored using AVEVA PI means.

These CSV files consisting of PI tags can be imported into PI.

---

<https://kb-hosting-cs.s3.us-east-1.amazonaws.com/KB/Optical-Diode/BlueStatsTags.csv>

<https://kb-hosting-cs.s3.us-east-1.amazonaws.com/KB/Optical-Diode/RedStatsTags_Collective.csv>

---

Blue Diode: Ensure you update the Tag Name in the CSV file and replace the 1 with the actual instance ID set in the NetWall UI.

For example, using the instance ID 100

i.e., opswat_blue_ 1_PointCount → opswat_blue_100_PointCount

Red diode: Tags can be imported. No change needed to tags.

#### [**Note**](/docs/netwalldiode/v1.13.2/knowledge-base/monitoring-status-performance-for-data-diodes-with-aveva-pi-tags#note)

In order for the Diode to publish statistics, it must be aware of the AVEVA PI Point Source, chosen for the zone.

The AVEVA PI Point Source in the CSV is set to 'OPSWAT'. It can be modified to another value. The source must be specified in the Diode config in order for the PI Tags to be updated. If it’s 'OPSWAT', then 'OPSWAT' needs to be entered as the PI Point Source in the Diode config.

#### [Example](/docs/netwalldiode/v1.13.2/knowledge-base/monitoring-status-performance-for-data-diodes-with-aveva-pi-tags#example)

To get information about each statistic tag, hover your mouse over the 'Info' icon to get a popup description.

If the administrator decides to replicate the Blue zone status/performance to the Red zone database, the Blue zone AVEVA PI Point Source must be named appropriately - for example ‘BLUE_100_ OPSWAT’. The corresponding AVEVA PI Point source must be added to the Red zone Point Sources tab.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

MetaDefender
