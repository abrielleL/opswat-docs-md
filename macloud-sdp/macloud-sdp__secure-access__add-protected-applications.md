<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/add-protected-applications -->

# Add Protected Applications

This feature requires a premium MetaDefender IT-OT Access License.

This section guides you through a workflow to protect your applications with SDP method. For testing purposes, OPSWAT hosts a demo application at [demo.sdp.opswat.com](http://demo.sdp.opswat.com)

- You will need to ensure that **Enable Secure Access** is checked off. This can be found in **Secure Access > Protected Apps**.
- Under **Secure Access**, click **Add Protected Application**, then choose **SDP Method**. To protect applications with the IdP Method, you can refer [Add protected applications with IdP Method](/docs/macloud-sdp/secure-access/add-protected-applications-with-idp-method).

## [Creating the protected application](/docs/macloud-sdp/secure-access/add-protected-applications#creating-the-protected-application)

- **Application Name**: this name will be shown to your end-users.
- **Access Mode**:

  - **Disable**: the system will always allow an authorized users to access the application without processing access rules on your account.
  - **Monitor**: the system will process access rules but will always allow an authorized users to access the application without processing access rules on your account.
  - **Enforce**: the system will process access rules to decide if the system grants an authorized users access to the application.
- **Application Type**: it can be an web application, SSH, RDP, or Other.

  - For **SSH, RDP, or Other** types of applications, MetaDefender IT-OT Access allows administrators to add up to 1,000 addresses to the protected application. For more information on bulk uploading addresses, please click [here](https://docs.opswat.com/macloud-sdp/secure-access/bulk-upload).
- **Application URL**: where the application is hosted.
- **Ports**: ports the application is running.
- Check **Allow ICMP Traffic** if you allow devices send ICMP traffic to the application.
- Check **Visible to Users** if you want to users to see the applications listed in the SDP section of the OPSWAT Client. Hidden applications will still be accessible to users according to your access rules.
- Click **Save.**

Note: For commonly used applications, please refer to [Commonly Used Application Setup](/docs/macloud-sdp/metaaccess-cloud-and-sdp/3.13.0/secure-access/common-used-application-setup)

## [User Assignment](/docs/macloud-sdp/secure-access/add-protected-applications#user-assignment)

- Assign who can access to this application. This step can be skipped and do later. Refer [Assign users groups to a protected application](/docs/macloud-sdp/secure-access/assign-users-groups-to-a-protected-application) for more details.
- Click the arrow icon to add to the selected Users/Groups lists to grant end-users/IdP groups access to the applications.
- Click **Assign.**

## [Gateways](/docs/macloud-sdp/secure-access/add-protected-applications#gateways)

- You may be asked to set up a SDP Gateway if you have not set up SDP Gateway, please refer [Set up an Secure IT Access Gateway](/docs/macloud-sdp/secure-access/set-up-an-sdp-gateway) for more details.
- Configure your firewall/proxy to lock the application down so only SDP Gateways can reach your application. At this step, the system will show available gateways on your account.
- Assign what gateways can access to this application. This step can be skipped and do later.
- Click the arrow icon to add the selected gateway(s) to the access list for applications.
- Click **Assign.**
