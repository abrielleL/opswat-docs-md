<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/universal-link -->

# Universal Link

OPSWAT Mobile App now supports scheme/universal link to provide a seamless way for you to link a custom id in your solution with a device id OPSWAT Mobile App generates for a device. By this way, your solution can use the custom id to query device details on MetaDefender IT-OT Access. Your app/website just needs to provide an OPSWAT Mobile App's universal link with a custom id as a parameter to end-users. By tapping the link, the universal link lets the user open the installed OPSWAT Mobile App and pass the custom id to the app. The OPSWAT Mobile App reports compliance data and links the custom id with the device id. Your solution can then use the [Device Details v3.2](/docs/macloud-sdp/developer-guide/device-details-v3-2) query the device details with the custom id.

**Universal Link Format**

https://mobile.metaaccess.opswat.com/<custom_id>?app_name=<APP_NAME>&app_id=<APP_ID>

**Scheme Link Format**

metaaccess://<custom_id>?app_name=<APP_NAME>&app_id=<APP_ID>

**Parameters**

| Parameter | Data Type | Description | Required |
| --- | --- | --- | --- |
| custom_id | string | a unique custom id you want to link to the device. If it's invalid, OPSWAT Mobile App fails to send a report to the MetaDefender IT-OT Access and shows the error code as 4000 Only accept a-z, A-Z, 0-9, and hyphen (-) characters. Maximum length is 50 characters | Yes |
| app_name | string | name of an app which you want to tell the user go back after opening OPSWAT Mobile App. After reporting compliance data to MetaDefender IT-OT Access successfully, OPSWAT Mobile App will show a message to tell the user to go back to that app. If this is invalid or missing, OPSWAT Mobile App just tells users go back to previous app | Optional |
| app_id | string | Android package name/iOS app scheme of the app which you want the user goes back. If this is invalid or missing, users need to go back to the desired app manually. Note that app_id is *case-sensitive.* See [How could I find an app ID of an application?](/docs/macloud-sdp/kb/how-could-i-find-an-app-id-of-an-application-)? | Optional |

**Common Error Codes**

The OPSWAT Mobile App will throw error message to end-users along with a specific error code.

| Error code | Error Description | Resolution |
| --- | --- | --- |
| 4000 | The custom id in the universal link is invalid |  |
| (No specific error code) | The OPSWAT Mobile app could not connect to the MetaDefender IT-OT Access server | 1. If a device is on a cellular network, please check if the OPSWAT Mobile app is allowed to use cellular data 2. Check if a mobile device can connect to the MetaDefender IT-OT Access servers which the app is connecting to. 3. If the server is up. |

**Example with an appID:**

**Scheme**

iOS: metaaccess://TEST67AD71?app_name=Salesforce&app_id=salesforce1://
Android: metaaccess://TEST67AD71?app_name=Salesforce&app_id=com.salesforce.chatter

**Universal Link**

iOS: https://mobile.metaaccess.opswat.com/TEST67AD71?app_name=Salesforce&app_id=salesforce1://
Android: https://mobile.metaaccess.opswat.com/TEST67AD71?app_name=Salesforce&app_id=com.salesforce.chatter

On the OPSWAT Mobile App, users will get a message like the one below after the app reports data to the MetaDefender IT-OT Access successfully.

**Example with an invalid custom id:**

iOS: https://mobile.metaaccess.opswat.com/TEST!?app_name=Salesforce&app_id=salesforce1://

On OPSWAT Mobile App, users will get the below error message.

**

#### [IMPORTANT NOTE](/docs/macloud-sdp/developer-guide/universal-link#important-note)

- Universal/Scheme link only works when users click on the URL link then the device OS will automatically handle the navigation to OPSWAT Mobile App. If copying and pasting the universal/scheme URL to the browser address bars, the OS won’t know and it won’t open the OPSWAT Mobile App. This happens on both Android and iOS.
- If the device does not install the OPSWAT Mobile App before clicking the URL, it will also direct to the device’s default browser.

**

**Browser Support Chart**

(Tested on iPhone XS max, iPad mini, Samsung, Nexus)

|  | iOS |  | Android |  |
| --- | --- | --- | --- | --- |
|  | Normal mode | Private mode | Normal mode | Private mode |
| Safari | Universal Link/ Scheme | Universal Link/ Scheme |  |  |
| Edge | Universal Link/ Scheme | Universal Link/ Scheme | Universal Link/ Scheme |  |
| Chrome | Universal Link/ Scheme | Universal Link/ Scheme | Universal Link/ Scheme | Scheme |
| Firefox | Universal Link/ Scheme | Universal Link/ Scheme | Scheme |  |
| Opera | Universal Link/ Scheme | Universal Link/ Scheme | Scheme |  |
| Samsung browser |  |  | Universal Link/ Scheme |  |

As June 15, 2018, MetaDefender IT-OT Access releases a new agent version on mobile devices which supports Universal Link

- iOS app version: 2.45.11+
- Anroid app version: 2.54.4+
