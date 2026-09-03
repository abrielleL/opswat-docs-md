<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-could-i-retrieve-client-id-and-client-secret-on-metaaccess-t -->

# How could I retrieve Client ID and Client Secret on MetaDefender IT Access to integrate with my NAC or SSL/VPN solution?

This article applies to the current MetaDefender IT Access oAuth Portal, all licensed MetaDefender IT Access accounts and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

Pro Tip:

MetaDefender IT Access integrates seamlessly with third-party products, such as Network Access Control, IPSEC VPN and SSL VPN, to provide advanced compliance data and compromised-device information that can inform the enforcement actions to be taken by such solutions.

Some third-party integrations require you to fill in the **MetaDefender Endpoint** **ID** and **Client Secret** during setup. To retrieve the necessary details, please follow the instructions below.

Please Note:

You will need to have a licensed MetaDefender IT Access account in order to begin registering your applications to our platform. To set one up, please contact the [OPSWAT Sales](https://www.opswat.com/contact) team.

With your account in place, you can proceed to registering your applications via the process below.

Following registration of your applications, the applications will be confirmed and the Client Key and Client Secret strings will be provided.

These keys are unique and should be stored for your eyes only.

1. Log into the **MetaDefender IT Access oAuth Porta**l, [Here](https://gears.opswat.com/o), using your standard MetaDefender IT Access Console login details.
2. Navigate to the **oAuth Applications** page and click **Register New Application** in the top, right-hand corner of the screen, as illustrated below.

3. On the **Application Settings** page, illustrated below, fill in all the necessary details in the fields provided, and upload the necessary file, including:

   - **Application Name**
   - **Description**
   - **Permission**
   - **Icon File**
   - **Website URL**
   - **Callback URL** - where the user is directed after authorizing an application for access to the account, for example: <http://127.0.0.1/opswat>.

Pro Tip:

For further guidelines on adding your application’s name, details and logo, please [Read Branding Guidelines](https://docs.opswat.com/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis).

4. Now, click **Create** to register your application.
5. Copy the **Client Key/ID** and **Client Secret**, as illustrated in the screenshot below.

Support:

For further queries, concerns or issues regarding the **Retrieval of A Client ID And Client Secret On** **MetaDefender IT Access , To Integrate With Your NAC Or SSL/VPN Solution**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
