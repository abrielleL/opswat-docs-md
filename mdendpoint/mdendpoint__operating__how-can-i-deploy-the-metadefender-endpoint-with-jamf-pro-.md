<!-- source: https://www.opswat.com/docs/mdendpoint/operating/how-can-i-deploy-the-metadefender-endpoint-with-jamf-pro- -->

# How can I deploy the MetaDefender Endpoint with Jamf Pro?

> **Check Your Product:**
>
> This article applies to all MetaDefender Endpoint releases deployed on macOS systems.

> **Pro Tip:**
>
> Jamf Pro is an IT administrative tool suite that offers automated and unified endpoint management for Apple devices.
>
> The Jamf Pro server can be used to deploy various software and utility packages through networks of managed endpoints simultaneously and, as such, can also be used to deploy the MetaDefender Endpoint to your managed macOS endpoints.

To deploy MetaDefender Endpoint to your macOS endpoints using Jamf Pro, please follow the preparation and deployment instructions below.

## [Preparation](https://docs.opswat.com/macloud-sdp/kb/how-can-i-deploy-the-opswat-client-with-jamf-pro-#preparation)

1. Ensure that your Jamf Pro server is up and running.
2. Ensure that all potential Client devices have the Jamf service running in the background.

## [Client side deployment](https://docs.opswat.com/macloud-sdp/kb/how-can-i-deploy-the-opswat-client-with-jamf-pro-#client-side-deployment)

1. First, you will need to save your account and group information to either the **.GlobalPreferences** file or the **com.opswat.GearsClientConfiguration** file. Whichever file you use, it must be stored by the Root user and opened by the Root user.
2. Open a Terminal, type **sudo su** then enter the root password when prompted.
3. Now, type cd /Library/Preferences and, once inside the folder, type the following:
   1. **defaults write .GlobalPreferences OwcServerCode** ***<server code here>*** to save your server code
   2. **defaults write .GlobalPreferences OwcLicenseKey <*****license key here*****>** to save your license key
   3. **defaults write .GlobalPreferences OwcGroupId <*****group ID here*****>** to save your group ID (optional)
   4. To delete a certain key (for example, if you no longer want to use the group ID you entered) please use the following command: **defaults delete .GlobalPreferences <*****the key to be deleted*****>**
   5. To test whether your values have been saved correctly, type: **defaults read .GlobalPreferences**

> **Pro Tip:**
>
> If you want to use the c**om.opswat.GearsClientConfiguration** file instead of **.GlobalPreferences** to set up your information, please substitute the file name in the commands below.

The screenshot below illustrates the process, with the information being stored in the **.GlobalPreferences** file.

![](https://uploads.developerhub.io/prod/1yda/9fkr91pbcukgv0ofbheab7xwc4tkm8bdmar4vk53d599821qz4mm3jn8d4l009ip.png)

## [Jamf server side deployment](https://docs.opswat.com/macloud-sdp/kb/how-can-i-deploy-the-opswat-client-with-jamf-pro-#jamf-server-side-deployment)

Ensure that all Client devices are connecting to the Jamf Pro server and, from the server side, follow the instructions below.

1. Add the MetaDefender Endpoint package to the Jamf server. [Read This](https://docs.jamf.com/10.37.0/jamf-pro/documentation/Packages.html) to learn more. a. In your Jamf Pro dashboard, navigate to **Settings: Computer Management>Package.** b. Click the **New** button.

c. Click **Choose File**.

d. Choose the **package file** you wish to upload, in this case, the MetaDefender Endpoint package file.

e. Click **Save**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/4zg6635deb2v10kbo4ept40brydhzpfqcgf6wsddzomwstxrssfreptbqnkw1bvw.png)

2. Next, you must add the Start OPSWAT App script to the Jamf Pro server. [Read This](https://docs.jamf.com/10.37.0/jamf-pro/documentation/Scripts.html) to learn more. a. In your Jamg Pro dashboard, navigate to **Settings: Computer Management>Scripts.** b. Click the **New** button.

c. Type the **name of the script** you wish to add, in this case, the name of the Start OPSWAT App script, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/1yda/a00n6v3lvdzfvymusmh5p29ulee7xgzxbfdler8avu1qla0j14y6s8xr1yz6nfju.png)

d. Click on the **Script** tab.

e. Paste the script in the field provided, ensuring that the mode of the script is **Shell/Bash**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/mjz2jauxa02apoh0vkqxbz3potl1h6mxex8mp1swyz7ikdvvonkez51jol94lqrk.png)

f. Now, click **Save**.

3. Next, you must create a Policy to cover the rules for deployment of Client across your endpoints. [Read This](https://docs.jamf.com/10.37.0/jamf-pro/documentation/About_Policies.html) to learn more. a. Click on the **Computer** icon in the top right-hand corner of your Jamf Pro dashboard. b. Click on **Policy**, then click the **New** button.

c. Type a **Display Name** for the policy in the field provided, and set the **Trigger** as **Start** or **Login**.

d. Set the **Scope** to include the necessary Client devices.

e. In the Package tab, add the uploaded script and set its Priority as After.

f. Finally, click **Save** to apply your changes.

g. Logout or restart the Client devices to deploy the package.

The script is illustrated in the screenshot below.

```cpp
Bash
#!/bin/bash
loggedInUser=$(stat -f%Su /dev/console)
loggedInUserUID=$(/usr/bin/id -u "$loggedInUser")
​
#unload
/bin/launchctl asuser "$loggedInUserUID" launchctl unload -wF /Library/LaunchAgents/com.opswat.GearsApp.plist
/bin/launchctl asuser "$loggedInUserUID" launchctl unload -wF /Library/LaunchAgents/com.opswat.GearsAppRunOnLogin.plist
​
#load
/bin/launchctl asuser "$loggedInUserUID" launchctl load -wFS Aqua /Library/LaunchAgents/com.opswat.GearsApp.plist
/bin/launchctl asuser "$loggedInUserUID" launchctl load -wFS Aqua /Library/LaunchAgents/com.opswat.GearsAppRunOnLogin.plist
​
fi
exit 0
```

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Deploying MetaDefender Endpoint Via Jamf Pro**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
