<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/endpoint-management/how-to-enable-copying-files-from-a-drive-to-a-removable-media- -->

# How to enable copying files from a drive to a removable media?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on Windows, Linux, macOS, iOS or Android systems.

As of **V7.8.0**, My OPSWAT includes a setting that allows administrators to Enable/Disable the MetaDefender Endpoint’s ability to report to  My OPSWAT when files from the system on which the Endpoint is installed are copied from that local drive to a removable media.

To make use of this setting, please follow the instructions below.

1. Log into your  **My OPSWAT Console** and navigate to **Device Policies>Relevant Policy**.
2. If **Threat Detecti**on is disabled, enable it by checking the box alongside **EnableThreat Detection**.

![](https://uploads.developerhub.io/prod/9jd0/upnaat576hojgherh3o1k6q4xu96k0suq8pzn0erkhjaodvl1nmttn27mzxopn67.png)

3. Under your **Threat Detection** settings, scroll down to the section on **Removable Media Protection** and check the selection box to enable the feature and open up the configuration options.

![](https://uploads.developerhub.io/prod/9jd0/gij3c6gwrkid385zsvvy5l210ymey9rckyi864t8ja4xpnf7vithot95ti5so7iu.png)

4. Now, check the option to **Allow a user to do selected actions**, as well as the options to **Copy files from a local/network drive to a removable media** and to **Report a copy result when a user copies files from local drives to a removable media**.

![](https://uploads.developerhub.io/prod/9jd0/ihpfwf88scv7sxslhcphm1jfed5v9qesmzo2kx5khon9gfwxisk9yrf9uc0eceol.png)

> **Success**
>
> With these settings enabled, the MetaDefender Endpoint on all devices under this policy will report to My OPSWAT whenever files from their respective local drives are copied to removable media. These reports can be downloaded (once logs have been fetched for a given device) via the **My OPSWAT Management Console>Inventory>Devices>Relevant Device>Events>Action Logs**, as illustrated in the screenshot below. For detailed instructions on retrieving device logs, please [Read This](https://docs.google.com/document/d/120ZjeV9v8yMrbBrdyRQlsDTUcF-jwavM24dAZkhx9h0/edit?usp=sharing).

![](https://uploads.developerhub.io/prod/2x2P/4hh3lhw0663oy8nrpgsragp550go1a1oathctni3qo0jsf1be42znr5aauw73itr.png)

5. Finally, in the lower right-hand corner of the screen, click the **Save** button to implement your settings.

> **Support:**
>
> If you have any difficulty **Enabling The Copying Of Files From A Drive To A Removable Media**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
