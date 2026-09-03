<!-- source: https://www.opswat.com/docs/cm/patch-management/air-gapped-patching---new-patch-management -->

# Air-Gapped Patching - New Patch Management

## **Setting up My OPSWAT Central Management On-Premises**

> **Info**
>
> Starting with My OPSWAT Central Management 10.6.2605, the **new Patch Management solution** is available and provides a unified approach to patching operations.
>
> To switch to new Patch Management solution, see [How to switch ](https://www.opswat.com/docs/cm/patch-management/on-premise-patch-management#how-to-switch-between-the-two-versions)guidelines.

To begin setting up the new air-gapped patch management solution, two things need to be done first:

1. My OPSWAT Central Management on-premises is [installed](https://www.opswat.com/docs/cm/deployment/msi-installation), licensed, and[ switched](https://www.opswat.com/docs/cm/patch-management/on-premise-patch-management#how-to-switch-between-the-two-versions) to the new Patch Management solution
2. Endpoint devices are [enrolled](https://www.opswat.com/docs/cm/product-management/metadefender-endpoint)

When endpoints are enrolled and communicating with My OPSWAT Central Management, they will begin to report their missing patches.

There are 2 places where missing patches can be viewed:

- For a singular device
  - Inventory > Devices > *selected device *> Patch Management

![](https://uploads.developerhub.io/prod/97qW/vii57115s6xf5bhi0a1kp18pkc2z2viudfb75kcdz1acgzlopxen22holrfbny6k.png)

- All missing patches aggregated among all devices
  - Patch Management > Patches > Operating System / Third Party Application tabs

![](https://uploads.developerhub.io/prod/97qW/qzygjphhjz5vbb2mhtylrqqbfbwfls8x29rzmbdjfll8riyv2u19sannllgrzc8o.png)

Refer to [Manage Missing Patches and Outdated Applications](https://www.opswat.com/docs/cm/patch-management/manage-missing-patches) for more details.

## **Patch Dashboard**

Patch Dashboard gives you a centralized view of OS and application patch posture, and deployment results across your environment. Use dashboard widgets to discover security gaps, prioritize what to fix first, and confirm your deployment outcome.

In the left navigation, select **Patch Management > Dashboard**

![](https://uploads.developerhub.io/prod/97qW/5d0iup8mvd33ohft755gphi14rrez1l5dmysgx2jj9ynp53ee9sfiqzyprsv99cv.png)

Refer to [Patch Dashboard](https://www.opswat.com/docs/cm/patch-management/patch-dashboard) for more details.

---

## **Enable air-gapped patching**

To enable Endpoints to retrieve patches from My OPSWAT Central Management:

1. Log in to My OPSWAT Central Management
2. Navigate to Patch Management > Upload Patches > Operating System / Third Party Application
3. Check "Enable Local Patch Repository"
4. Click the Save button to apply

![](https://uploads.developerhub.io/prod/97qW/l8vd9m7aeyblzzkjqya60x32gjlnfhv1bnf74zybt2fv7td6mts0x3icnrgcsrog.png)

> **Obtaining patch packages**
>
> Your vendor, in partnership with OPSWAT, will provide the capability to download patch packages to upload & distribute via My OPSWAT Central Management to MD Endpoints.
>
> Contact your vendor for further information on how to obtain patch packages.
>
> If you are an ICS vendor looking to provide patch packages for your customers, please contact [OPSWAT ](https://www.opswat.com/support)directly to enable the operation.

---

## **Upload patches to distribute**

Patch packages are delivered in two pieces:

- .zip package containing the patch content
- .yml descriptor file for validating the .zip package

There are 2 modes for providing patches:

1. Manual
2. Folder

![](https://uploads.developerhub.io/prod/97qW/erfmhdytz2jcbve6sxb6xyd4bv2ub8hkgl4dlo3p8qn2zatmm4eomhrktsul2yfm.png)

### Manual

![](https://uploads.developerhub.io/prod/97qW/rdif1vjsno4dcuyda3xzf13kn7a5n1v7dzplrhpio1294gtrsd0crq15ol60pj7x.png)

When selected, additional boxes are displayed for the upload:

- **Select yml and zip files to update**
  - click the upload icon to browse for the yml (descriptor) and zip (package) file to upload
- **Applicable Groups**
  - set the specific groups the patches being uploaded will be applicable for
  - this setting informs if a patch setting configuration is valid, if the deployment includes a disallowed group or devices that are within a disallowed group
  - default setting: All groups

As patch packages are uploaded, My OPSWAT Central Management will validate the package with the descriptor file.

All uploaded patches will be listed out after upload:

![](https://uploads.developerhub.io/prod/97qW/irw64q80j6dpuej12mc4yj8t26iauia28rn1vgmzqjo1wk31vcoe1oixlt949qqv.png)

### **Folder**

![](https://uploads.developerhub.io/prod/97qW/cneleg4fdtccnyz9fzxlz3125xink38auedwvdatp0limkesozagu9h3w1x1qzwz.png)

When selected, a Patch Repository Location is displayed. The path is local to the system My OPSWAT Central Management is installed on.

All patches are expected to be stored in this directory, under a distinct structure outlined below.

Simply copy and paste the patches to the location configured.

Admins need to maintain the following directory structure in the specified format for My OPSWAT Central Management to correctly identify patches:

![](https://uploads.developerhub.io/prod/97qW/3q02u7b30agrxeg6bxuf39r3korw79zjefad17te1ytv4c4ciqhybju7e89kr26c.png)

---

## **Configure Patch Deployments**

Once patches are uploaded, you can create and configure patch deployments.

Choose a deployment method based on your target devices and intended purpose, then configure the deployment accordingly.

| Deployments | Details | Configure Deployment |
| ---- | ---- | ---- |
| On-Demand Deployment  | Pushes patches to targeted endpoints immediately. Use it for urgent security fixes, critical vulnerabilities, or targeted updates. | [Configure On-Demand Deployment](https://www.opswat.com/docs/cm/patch-management/on-demand-deployment#configure-on-demand-deployment) |
| Policy Deployment | Installs patches automatically on a repeating schedule, without manual deployment triggering. | [Configure Policy Deployment](https://www.opswat.com/docs/cm/patch-management/policy-deployment#configure-policy-deployment) |
| Ring Deployment | Roll out patches in stages before deploying broadly. Use it to reduce risk when patching large or sensitive environments. | [Configure Ring Deployment](https://www.opswat.com/docs/cm/patch-management/create-ring-deployment#configure-ring-deployment) |

---

## **Configure a Cache Node**

By default, all Endpoints will reach out to My OPSWAT Central Management to download and apply patches.

This can introduce a large bottleneck on the server if there are many Endpoints enrolled for management.

To reduce this load, Endpoints can be selected to serve as a **Cache Node** to help distribute patches to other Endpoints instead if solely relying on My OPSWAT Central Management.

Cache Nodes support distributing patches to configured device groups. Up to 2 devices can serve as a Cache Node for a specific group. A single Cache Node can span multiple groups.

> **Requirements for an endpoint to be set as a Cache Node:**
>
> - Visible to other MetaDefender Endpoint on a network
> - Sufficient free disk space for caching
>
> **Disk requirement:**
>
> - Disk available needed: 10 GB (65% free disk space)
>
> **Note: **A firewall inbound rule for TCP port 8443 will be created

To configure an Endpoint as a Cache Node, navigate to Inventory > Devices > *select device to set*.

On the device's details page, open the **Actions** dropdown in the top right corner and select **Set as Cache Node**.

A dialog menu will open describing the requirements and important information:

![](https://uploads.developerhub.io/prod/97qW/ddz5409yh6iq5vk48xoljnjqjt2h9mm78elqdpf23uhu5t2jwvsfu4j30xblewa8.png)

To set the device as a Cache Node, select the Groups for which the device will serve as a node. Check the acknowledgement and click Save.

### **View which device is a Cache Node**

Verifying which device is a cache node can be seen in a device's **System Information**:

![](https://uploads.developerhub.io/prod/97qW/ydxoyv663jv0f11oschv5uqy4d4xtzjnvym3wjwx86ie806okr26oxyngvcf2ua4.png)

![](https://uploads.developerhub.io/prod/97qW/pd8fyufqnkpm19ds985ynbpp97g1rm227ztdicnzlrvavpevtm325zjyi21dkau0.png)

### **Remove a Cache Node**

To remove an Endpoint as a Cache Node, navigate to Inventory > Devices > *select device to set*.

On the device's details page, open the **Actions** dropdown in the top right corner and select **Set as Cache Node**.

In the dialog menu, de-select the configured groups, check the acknowledgement, and click Save.

---

## **Update Patch database definitions**

My OPSWAT Central Management comes pre-bundled with vulnerability and patch management definitions.

These databases will be downloaded by MetaDefender Endpoint when it syncs with the management server. They enable the ability for Endpoint to scan the local system and identify what patches are missing and vulnerabilities associated with versions installed on the system.

To ensure identification is up to date, new definitions can either be downloaded from your vendor or from My OPSWAT Portal.

Definitions can then be uploaded in Updates > Endpoint Components > Vulnerability Definitions / Patch Management

![](https://uploads.developerhub.io/prod/97qW/wsekptt0izf2jakz3p52ww2ygqtyw2djf1d663ja87e7w2yzq0teh4x5a0tip34x.png)

---

## **Patch Reports & Notifications**

Patch Reports & Notifications provides administrators with the centralized tools to maintain full visibility into patch compliance, communicate patch posture to stakeholders, and receive timely alerts for critical patching events, all from within My OPSWAT Central Management.

![](https://uploads.developerhub.io/prod/97qW/2jvo2opt4xalivd0whqgbyobul9eqsvuyuiv2lnabe6224tvb2uawqpdab1i54sk.png)

![](https://uploads.developerhub.io/prod/97qW/mult7gds8ipkoc6fxc6dbxc6a4kwzl1qvorlaxbutvhnn1ckko7phpmpzzkmrk74.png)

Refer to [Patch Reports & Notifications](https://www.opswat.com/docs/cm/patch-management/patch-reports---notification) for more details.
