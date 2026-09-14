<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/what-can-i-do-if-metadefender-core-shows-a-high-number-of-files- -->

# What can I do if MetaDefender Core shows a high number of files that failed to scan?

This article applies to all MetaDefender V5 releases deployed on Windows or Linux systems.

**Context**

This can be due to several different factors, some of which can be figured out and remediated on a DIY basis, and several of which can only be discovered by OPSWAT Support after you open a Support case. Instructions below.

Mostly it comes down to, one or more of Core’s engines are offline or updating during the time the scan is performed.

**Set the failure threshold**

Under normal circumstances, all active engines scan every file.

However, there are some situations in which scanning might be impacted and a “failed to scan” result is observed. In such situations, the behavior may be caused by a number of factors:

- Some engines failed to scan, and exceeded the scan failure threshold settings in place on the Core side.
- Core itself has a fatal problem e.g. Core service crashed.
- Due to configurations:

  - Failed the scan when sanitization timeout or failed.
  - Failed the scan when archive extraction failed.

Please Note:

MetaDefender V5 includes an option that modifies the behavior of the product when a specific engine fails to scan - such as in the case mentioned above.

Here, MetaDefender Core can be configured to fail the scan if any of the engines report problems. In other words, it can toss out all partially complete scans.

Failing to disable this option can give the illusion that MetaDefender Core is failing to scan large amounts of files.

**MetaDefender Core V5 Releases**

To disable this option on V5, follow these steps:

1. In your web browser, navigate to the MetaDefender Core **Management Console** at <http://localhost:8008/> (you may need to log in under admin privilege)
2. On the left menu, navigate to **Workflow Management → Workflow** to list all available rules
3. Click on a workflow you are using for the current scan to modify the setting
4. Click on the **Metascan** tab

Uncheck the option **Scan Failure Threshold** shown below.

**If that didn’t fix it**

With separate update windows for anywhere from 4 to 20 AV engines, and separate update windows for each of the utility engines, this could result in periods throughout the day where multiple engines are sporadically unavailable.

To minimize the impact of these updates, you can ensure that all engines are set to update **outside of peak hours**. This can be done from the Settings menu > Module Updates. Just pick one or more blackout windows to exclude the times when you expect the most scan volume, as shown below.

**Dependencies**

If the errors persist, it’s possible Core may be missing a dependency. Typically, this will be the latest C++ redistributable.

Please install the latest C++ package for your platform from the Microsoft website and then restart the MetaDefender Core service.

Once Core is online again, please monitor whether the Failed to Scan errors persist.

If they do, it’s time to open a Support case.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
