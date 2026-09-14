<!-- source: https://www.opswat.com/docs/ocm/7.39.0/knowledgebase/how-to-enable-copying-files-from-a-drive-to-a-removable-media -->

# How to enable copying files from a drive to a removable media

This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

As of **V7.8.0**, OPSWAT Central Management includes a setting that allows administrators to Enable/Disable the MetaDefender Endpoint’s ability to report to OPSWAT Central Management when files from the system on which the Client is installed are copied from that local drive to a removable media.

To make use of this setting, please follow the instructions below.

1. Log into your **OPSWAT Central Management Console** and navigate to **Device Policies>Relevant Policy**.
2. If **Threat Detecti**on is disabled, enable it by checking the box alongside **EnableThreat Detection**.

3. Under your **Threat Detection** settings, scroll down to the section on **Removable Media Protection** and check the selection box to enable the feature and open up the configuration options.

4. Now, check the option to **Allow a user to do selected actions**, as well as the options to **Copy files from a local/network drive to a removable media** and to **Report a copy result when a user copies files from local drives to a removable media**.

Pro Tip:

With these settings enabled, the MetaDefender Endpoints on all devices under this policy will report to OPSWAT Central Management whenever files from their respective local drives are copied to removable media. These reports can be downloaded (once logs have been fetched for a given device) via the **OPSWAT Central Management Console>Inventory>Devices>Relevant Device>Events>Action Logs**, as illustrated in the screenshot below.

For detailed instructions on retrieving device logs, please [Read This](https://docs.google.com/document/d/120ZjeV9v8yMrbBrdyRQlsDTUcF-jwavM24dAZkhx9h0/edit?usp=sharing).

5. Finally, in the lower right-hand corner of the screen, click the **Save** button to implement your settings.

Support:

If you have any difficulty **Enabling The Copying Of Files From A Drive To A Removable Media**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
