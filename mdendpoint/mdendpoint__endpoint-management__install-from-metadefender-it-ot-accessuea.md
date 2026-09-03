<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/install-from-metadefender-it-ot-accessuea -->

# Installed from MetaDefender IT-OT Access

## Installing MetaDefender Endpoint directly

1. Log into your **MetaDefender IT-OT Access Console**.
2. Click the **+Device** button, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/gc1t88zo5f68mdowyp80aefbrpgyu8rjspfydbr7xw68gsttqkk8vdymfnt4f3rh.png)

3. In the pop-up window, click the link to **Download MetaDefender Endpoint For Distribution**, as illustrated below.

> **Pro Tip:**
>
> This download link is **shareable** and can be distributed to your endpoint users with your instruction to download the installer and install the package themselves.

![](https://uploads.developerhub.io/prod/2x2P/pqy2lthzgp6ygpcc6k29oojy67k7q1yu9ho5bfj66xhoedtr1ogls30f5ufdm4nf.png)

## [Pushing Client deployment via Active Directory](https://docs.opswat.com/macloud-sdp/3.39.0/kb/how-do-i-deploy-or-distribute-opswat-client-to-my-devices-#pushing-client-deployment-via-active-directory)

4. Identify and create a network share location, then copy the downloaded Client Package to that location, without changing the package filename.
5. Log into Active Directory’s **Group Policy Management Console**.
6. From the GPMC, create a **GPO** with appropriate scope, then link it to an **OU**.
7. Create your software installation for **Computer Configuration** and/or **User Configuration**, providing the full **UNC path** to the MetaDefender Endpoint package file.
8. Enable and deploy the policy via Active Directory. For further instructions, please [Read This](https://docs.opswat.com/macloud-sdp/kb/can-i-use-active-directory-to-distribute--enforce-or-audit-opswa).

> **Expand:**
>
> If you have reached the maximum number of devices that can be monitored on your account, please contact the **OPSWAT Sales Team** [Here](https://www.opswat.com/contact) to purchase additional devices and expand your manageable network.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Deploying Or Distributing** **MetaDefender Endpoint** **To Your Endpoint Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
