<!-- source: https://www.opswat.com/docs/macloud-sdp/kb/how-do-i-deploy-or-distribute-opswat-client-to-my-devices- -->

# How do I deploy or distribute MetaDefender Endpoint to my devices?

This article applies to all MetaDefender IT Access products deployed on Windows, macOS, Linux, Android and iOS systems.

There are various methods for deploying/distributing MetaDefender Endpoint to your managed endpoint devices.

This article will cover the most common methods, including:

- Installing MetaDefender Endpoint directly onto devices.
- Pushing deployment via Active Directory.

Other common methods include:

- Adding Client directly to your Golden Image for new systems. For instructions on how to create a Golden Image containing the MetaDefender Endpoint, please [Read This](/docs/macloud-sdp/kb/can-opswat-client-be-distributed-using-a-golden-image--cloned-vm).
- Distributing MetaDefender Endpoint with your software deployment/distribution tool.

## [Installing MetaDefender Endpoint directly](/docs/macloud-sdp/kb/how-do-i-deploy-or-distribute-opswat-client-to-my-devices-#installing-metadefender-endpoint-directly)

1. Log into your **MetaDefender IT Access Console**.
2. Click the **+Device** button, as illustrated in the screenshot below.

3. In the pop-up window, click the link to **Download MetaDefender Endpoint For Distribution**, as illustrated below.

Pro Tip:

This download link is **shareable** and can be distributed to your endpoint users with your instruction to download the installer and install the package themselves.

## [Pushing Client deployment via Active Directory](/docs/macloud-sdp/kb/how-do-i-deploy-or-distribute-opswat-client-to-my-devices-#pushing-client-deployment-via-active-directory)

1. Log into your **MetaDefender IT Access Console**.
2. Click the **+Device** button, as illustrated in the screenshot below.

3. In the pop-up window, click the link to **Download MetaDefender Endpoint For Distribution**, as illustrated below.

4. Identify and create a network share location, then copy the downloaded Client Package to that location, without changing the package filename.
5. Log into Active Directory’s **Group Policy Management Console**.
6. From the GPMC, create a **GPO** with appropriate scope, then link it to an **OU**.
7. Create your software installation for **Computer Configuration** and/or **User Configuration**, providing the full **UNC path** to the MetaDefender Endpoint package file.
8. Enable and deploy the policy via Active Directory. For further instructions, please [Read This](/docs/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa).

Expand:

If you have reached the maximum number of devices that can be monitored on your account, please contact the **OPSWAT Sales Team** [Here](https://www.opswat.com/contact) to purchase additional devices and expand your manageable network.

Support:

If you have followed the instructions above but are having difficulty **Deploying Or Distributing** **MetaDefender Endpoint** **To Your Endpoint Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
