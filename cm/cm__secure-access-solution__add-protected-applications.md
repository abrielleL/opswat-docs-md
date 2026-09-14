<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/add-protected-applications -->

# Add Protected Applications

> **Info**
>
> This feature requires a premium My OPSWAT Central Management License.

This section guides you through a workflow to protect your applications with SDP method. For testing purposes, OPSWAT hosts a demo application at [demo.sdp.opswat.com](http://demo.sdp.opswat.com)

- You will need to ensure that **Enable Secure Access** is checked off. This can be found in **Secure Access > Protected Apps**.

![](https://uploads.developerhub.io/prod/97qW/3xcvx8db4yjszpg6r6rz3k7ayx4p42u38pcmurj3vrj94h1bg6hcf3rv1olrynz5.png)

- Click **Add Protected Application**, then choose **SDP Method**. To protect applications with the IdP Method, you can refer [Add Protected Applications with IdP Method.](https://www.opswat.com/docs/cm/secure-access-solution/SAML-SSO-add-protected-applications)

![](https://uploads.developerhub.io/prod/97qW/ctxo3s624jvhtjkpumnh7nmycww3web010axxjutr4gvx8dz95agjpr3yodil9d6.png)

## Creating the protected application

- **Application Name**: this name will be shown to your end-users.
- **Access Mode**:
  - **Disable**: the system will always allow an authorized users to access the application without processing access rules on your account.
  - **Monitor**: the system will process access rules but will always allow an authorized users to access the application without processing access rules on your account.
  - **Enforce**: the system will process access rules to decide if the system grants an authorized users access to the application.
- **Application Type**: it can be an web application, SSH, RDP, or Other.
  - For **SSH, RDP, or Other** types of applications, My OPSWAT Central Management allows administrators to add up to 1,000 addresses to the protected application. For more information on bulk uploading addresses, please refer to [Bulk Upload](https://www.opswat.com/docs/cm/secure-access-solution/bulk-upload).
- **Application URL**: where the application is hosted.
- **Ports**: ports the application is running.
- Check **Allow ICMP Traffic** if you allow devices send ICMP traffic to the application.
- Check **Visible to Users** if you want to users to see the applications listed in the SDP section of the OPSWAT Client. Hidden applications will still be accessible to users according to your access rules.
- Click **Save.**

Note: For commonly used applications, please refer to [Common Used Applications](https://www.opswat.com/docs/cm/secure-access-solution/common-used-applications) guideline.

## User Assignment

- Assign who can access to this application. This step can be skipped and do later. Refer [Assign Users/Groups to a Protected Application](https://www.opswat.com/docs/cm/secure-access-solution/assign-users-groups-to-a-protected-application) for more details.
- Click the arrow icon to add to the selected Users/Groups lists to grant end-users/IdP groups access to the applications.
- Click **Assign.**

## Gateways

- You may be asked to set up a SDP Gateway if you have not set up SDP Gateway, please refer [Set Up Gateways](https://www.opswat.com/docs/cm/secure-access-solution/set-up-gateways) for more details.
- Configure your firewall/proxy to lock the application down so only SDP Gateways can reach your application. At this step, the system will show available gateways on your account.
- Assign what gateways can access to this application. This step can be skipped and do later.
- Click the arrow icon to add the selected gateway(s) to the access list for applications.
- Click **Assign.**
