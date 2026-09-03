<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-could-i-retrieve-client-id-and-client-secret-on-my-opswat-ce -->

# How could I retrieve Client ID and Client Secret on My OPSWAT Central Management to integrate with my NAC or SSL/VPN Solution?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management oAuth Portal, all licensed My OPSWAT Central Management accounts and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

> **Pro Tip:**
>
> My OPSWAT Central Management integrates seamlessly with third-party products, such as Network Access Control, IPSEC VPN and SSL VPN, to provide advanced compliance data and compromised-device information that can inform the enforcement actions to be taken by such solutions.

Some third-party integrations require you to fill in the **Client** **ID** and **Client Secret** during setup. To retrieve the necessary details, please follow the instructions below.

> **Please Note:**
>
> You will need to have a licensed My OPSWAT Central Management account in order to begin registering your applications to our platform. To set one up, please contact the [OPSWAT Sales](https://www.opswat.com/contact) team.
>
> With your account in place, you can proceed to registering your applications via the process below.
>
> Following registration of your applications, the applications will be confirmed and the Client Key and Client Secret strings will be provided.
>
> These keys are unique and should be stored for your eyes only.

1. Log into the My OPSWAT Central Management console and click your account **Name** in the top, right-hand corner of the screen, select **OAuth Application** menu to access oAuth Portal.
2. Navigate to the **oAuth Applications** page and click **Register New Application** in the top, right-hand corner of the screen, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/fxeex8z9jxhxznftflqmnb8t6ls6ddk34x2n8e6uw48slw01uxjnr4axcmgor4ke.png)

3. On the **Application Settings** page, illustrated below, fill in all the necessary details in the fields provided, and upload the necessary file, including:
   - **Application Name**
   - **Description**
   - **Permission**
   - **Icon File**
   - **Website URL**
   - **Callback URL** - where the user is directed after authorizing an application for access to the account, for example: [http://127.0.0.1/opswat](http://127.0.0.1/opswat).

> **Pro Tip:**
>
> For further guidelines on adding your application’s name, details and logo, please [Read Branding Guidelines](https://docs.opswat.com/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis).

![](https://uploads.developerhub.io/prod/97qW/mssi0w5lg6hyydpggmcrnitek2g3c7y5pjjpb0zaydol4nfk9znj6xsnwfbp13zt.png)

4. Now, click **Create** to register your application.
5. Copy the **Client Key/ID** and **Client Secret**, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/if9ef61npkvhsnho9s6pgfqsi58kzsrw0c2nub55n9mc31qpvli26s8p4ob3ngud.png)

> **Support:**
>
> For further queries, concerns or issues regarding the **Retrieval  of A Client ID And Client Secret On** **My OPSWAT Central Management , To Integrate With Your NAC Or SSL/VPN Solution**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
