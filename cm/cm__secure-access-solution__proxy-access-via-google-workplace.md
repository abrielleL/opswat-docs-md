<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/proxy-access-via-google-workplace -->

# Proxy access via Google Workplace

My OPSWAT Central Management utilizes a secure access method called proxy-based access. This method uses a combination of proxies to provide device compliance based access control to applications that can limit access based on location. This approach is designed with Google Workspace Context-Aware Access  (IP Based).

*Note:*

- *For this feature to work, cross-domain API must be enabled and the port set to 1139. For more information on cross-domain API, click *[*here*](https://docs.opswat.com/macloud-sdp/developer-guide/cross-domain-api)*.*
- *The minimum OPSWAT agent version to support proxy-based access control is: 7.6.2301.163 (Windows only).*
- _Supported Google Workspace editions for this feature: [Enterprise](https://support.google.com/a/answer/10382130); Education Standard and Education Plus; Cloud Identity Premium. _[*Compare your edition*](https://support.google.com/a/answer/6043385)

To enable this feature on Google Workspace:

- In the Admin console, go to **Menu > Security > Access and data control > Context-Aware Access**.
- Click **Turn On**.

![](https://uploads.developerhub.io/prod/1yda/u3ypykais1k4tqt7slhyjcb7g5hawj0an9v069jl4ivggck39swshpospoh0hqv4.png)

Once enabled, create an **access level** that allows access only from the specific IP address:

- In the **Context-Aware Access** page, click **Create access level**.
- In the **Access level name** field, enter a name for the access level.
- In the **Mode** field, select **Basic mode**.
- In the **Context Conditions** section, click **Add condition**.
- In the **Condition type** drop-down list, select **IP subnet**.
- Enter the specific IP address that you want to allow access from.
- Click **Create**.

![](https://uploads.developerhub.io/prod/1yda/qehxbzkg78brkw8iar1ki1ua0rq88tgqtil69y23upuf0to8w7kxala52nmdz8vr.png)

Once you have created the **access level**, you can assign it to one or more apps with scope all users or a specific group of users:

- Go to the **Assign access levels** page and select the apps to assign the access level to.
- Select the **Access level** conditions (by IP address) created before, and click **Continue**.
- Select enforcement settings, , and click **Continue**.
- Review, and click **Assign**.

![](https://uploads.developerhub.io/prod/1yda/znordj9pxs0nlw17hycaaut2zpboyqvpkf3s0qqeao2hze1j83isonv2vepxyj80.png)

![](https://uploads.developerhub.io/prod/1yda/8rom6xvpga0db5nqeiq6ztpzfh3x6y796g6w02638zwxr6nhvs6zcpfk674wh6k6.png)

After creating this policy, My OPSWAT Central Management will be able to determine access to Google Workspace products based on the device's compliance state.
