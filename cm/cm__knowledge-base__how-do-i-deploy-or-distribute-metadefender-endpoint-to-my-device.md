<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-deploy-or-distribute-metadefender-endpoint-to-my-device -->

# How do I deploy or distribute MetaDefender Endpoint to my devices?

There are various methods for deploying/distributing MetaDefender Endpoint to your managed endpoint devices.

This article will cover the most common methods, including:

- Installing MetaDefender Endpoint directly onto devices.
- Pushing deployment via Active Directory.

Other common methods include:

- Adding Client directly to your Golden Image for new systems. For instructions on how to create a Golden Image containing the MetaDefender Endpoint, refer to [Can MetaDefender Endpoint be distributed using a golden image, cloned VMs or AMIs?](https://www.opswat.com/docs/cm/knowledge-base/can-metadefender-endpoint-be-distributed-using-a-golden-image--c)
- Distributing MetaDefender Endpoint with your software deployment/distribution tool.

## Installing MetaDefender Endpoint directly

1. Log into your **Console**.
2. Click the **+Device** button, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/aqjsnoor53pz2n239z62383qxuf3731nt1erq38lbg1hba9p3visqtxwhjwmwb8n.png)

3. In the pop-up window, click the link to **Download MetaDefender Endpoint For Distribution**, as illustrated below.

> **Pro Tip:**
>
> This download link is **shareable** and can be distributed to your endpoint users with your instruction to download the installer and install the package themselves.

![](https://uploads.developerhub.io/prod/97qW/23cfk0qn583hdjyzc9vyd4bqe2gsxcbn37x6op3l9yhx7bk27ofx7mvlbl45dfl2.png)

## Pushing Client deployment via Active Directory

1. Log into your **Console**.
2. Click the **+Device** button, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/tvmdm4feyi840c1biy6bbny49w4jpwx7x3vcmrrziuv4o7uhmoz38ayqrffero0s.png)

3. In the pop-up window, click the link to **Download MetaDefender Endpoint For Distribution**, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/qy3goizgeolc27z8n7ri8vuk3nz68bzai42bvxrmxnzgwoxhdg86l2b6pwk5v17w.png)

4. Identify and create a network share location, then copy the downloaded Client Package to that location, without changing the package filename.
5. Log into Active Directory’s **Group Policy Management Console**.
6. From the GPMC, create a **GPO** with appropriate scope, then link it to an **OU**.
7. Create your software installation for **Computer Configuration** and/or **User Configuration**, providing the full **UNC path** to the MetaDefender Endpoint package file.
8. Enable and deploy the policy via Active Directory. For further instructions, please refer to [How can I synchronize devices from Active Directory to My OPSWAT Central Management account?](https://www.opswat.com/docs/cm/knowledge-base/how-can-i-synchronize-devices-from-active-directory-to-my-opswat)

> **Expand:**
>
> If you have reached the maximum number of devices that can be monitored on your account, please contact the **OPSWAT Sales Team** [Here](https://www.opswat.com/contact) to purchase additional devices and expand your manageable network.

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Deploying Or Distributing** **MetaDefender Endpoint** **To Your Endpoint Devices**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
