<!-- source: https://www.opswat.com/docs/cm/configurations/certificates-management -->

# Certificates Management

The Certificate Management feature in My OPSWAT Central Management enables administrators to manage digital certificates across their environment. This includes importing, managing, and deleting certificates, as well as assigning them to product instances or policies.

**Supported Products**

- MetaDefender Core
- MetaDefender Kiosk K-Series

- [Certificate List Page](https://www.opswat.com/docs/cm/configurations/certificates-management#certificate-list-page)
- [Importing a Certificate](https://www.opswat.com/docs/cm/configurations/certificates-management#importing-a-certificate)
- [Certificate Details Page](https://www.opswat.com/docs/cm/configurations/certificates-management#certificate-details-page)
  - [Information tab](https://www.opswat.com/docs/cm/configurations/certificates-management#information-tab)
  - [Distribution Tab](https://www.opswat.com/docs/cm/configurations/certificates-management#distribution-tab)
- [Assigning a Certificate](https://www.opswat.com/docs/cm/configurations/certificates-management#assigning-a-certificate)
  - [Assign to Instance](https://www.opswat.com/docs/cm/configurations/certificates-management#assign-to-instance)
  - [Assign to Policy](https://www.opswat.com/docs/cm/configurations/certificates-management#assign-to-policy)
- [Unassign and Force Unassign a Certificate](https://www.opswat.com/docs/cm/configurations/certificates-management#unassign-and-force-unassign-a-certificate)
- [Delete a Certificate](https://www.opswat.com/docs/cm/configurations/certificates-management#delete-a-certificate)
- [Local Certificate](https://www.opswat.com/docs/cm/configurations/certificates-management#local-certificate)

## Certificate List Page

The Certificate List page displays all certificates imported into My OPSWAT Central Management.

- To access the page, navigate to **Settings → Certificates**.
- Each certificate includes the following details: Name, Status, Subject, Distribution, Version, Valid From, Valid To.

![](https://uploads.developerhub.io/prod/97qW/9nibamulvjqxxrfclt2ek8lppquabcmmlsqvkqv4ucd0jd4dhst8lt7rybeajlyd.png)

## Importing a Certificate

From the Certificate List page, click **Import Certificate**.

![](https://uploads.developerhub.io/prod/97qW/djqj13u21haj62ar1zpox4r5eo61sk67t6eb7yp2plo6q3kkw9saxoj117gt2hn0.png)

In the popup dialog:

- Enter a Certificate Name
- Upload the certificate file and private key (e.g., `.pem`, `.crt`, `.pfx`).
- If the private key is encrypted, enter the passphrase

Click **Add** to complete the import. Once imported, the certificate will appear in the Certificate List.

## **Certificate Details Page**

To view certificate details, select a certificate from the list.

### **Information tab**

![](https://uploads.developerhub.io/prod/97qW/cffwhcorpyapp9ch7be7o7er5jgf0818k8ccg7570pfuwcrjs7z85x5r31nlp433.png)

- Displays key certificate information.
- **Supported actions**: From the **Select Action** dropdown, you can:
  - **Assign to Instance**: Assign the certificate to a specific instance.
  - **Assign to Policy**: Assign the certificate to a policy, which can then be applied to one or more groups.
  - **Download**: Download the certificate for local use or backup.
  - **Delete**: Remove the certificate permanently.

### **Distribution Tab**

![](https://uploads.developerhub.io/prod/97qW/whvhm23pjs10gxi0sus6290xbo39637zn5inxklqyndehwahen6wiwn11lo5n20l.png)

Shows where the certificate is currently assigned. Each entry includes:

- **Name**: The name of the instance or policy.
- **Type**: Indicate the distribution type: the certificate can be assigned to a policy, device, or service.
- **Product**: Specify the OPSWAT product associated with the certificate.
- **Assigned By**: The user assigned the certificate.
- **Management Status**: Shows the current distribution status, which can be:
  - **Assigned**: The certificate is successfully assigned.
  - **Unassigning**: User has unassigned the certificate. My OPSWAT Central Management will request the device or instance to fully remove the certificate.
  - **Unassign Failed**: The unassign process failed; hover to the status to see the failure reason and view details.
- **Assign Date**: The date the certificate was assigned.

![Hover to Unassign Failed status to see failure reason and view details.](https://uploads.developerhub.io/prod/97qW/gd5x0rzpjjzx7ilx2rjgy6lnxwfih1g3nk2f7mscs89iza5k3kxvgg4bc82ndk5a.png)

## Assigning a Certificate

You can assign certificates from two places:

- **Certificate List Page:** Click the 3-dot menu → Select **Assign to Instance** or **Assign to Policy**.
- **Certificate Details Page**: Use the **Select Action** dropdown → Select **Assign to Instance** or **Assign to Policy**.

![](https://uploads.developerhub.io/prod/97qW/2klicec453rgwg5q3e2twvs8xs3e2pbekpc4t7bg62ir2z3fwd3qc77l28mjovvu.png)

### **Assign to Instance**

Use this method when each individual instance requires a unique, distinct digital certificate.

Assigning a certificate to an instance is a **two-step process:**

1. **Assign the certificate** to the target instance.
2. **Enable HTTPS on the instance to**  activate the certificate.

#### **MetaDefender Core**

**Step 1: Assign the certificate to the target instance**

- Select **Assign to Instance** → choose **MetaDefender Core**
- Choose your target Core instance from the list, and click **Assign**.

![](https://uploads.developerhub.io/prod/97qW/0ch26flu1kw9vrckvaa4o7o5ib238wyircs379m27nr6gupz4szjerbpgapvoz6e.png)

**Step 2**: **Enable HTTPS on the instance configuration**

- Navigate to **Inventory > Services** and open the target Core instance details.
- Go to the **Configuration** tab, under the **General** section, select **Security**.

![](https://uploads.developerhub.io/prod/97qW/pgxv6qttcfwmusa114zub7lhuufrj55fikrybxn3355sn50nbesu0fodrxk4c7ek.png)

- Click **Edit**, then select **Details**, toggle **Enable certificate**, select the target certificate from the dropdown selection, and click **Save changes**.

![](https://uploads.developerhub.io/prod/97qW/xy3jcp3t2etn2jv5r5btgjhmhnjcmtyul6p54v9qh7jr4vkqib84ew5yokbs8j36.png)

Note Only certificates listed in the instance’s **Certificates tab** are available for selection.

#### **MetaDefender Kiosk K-Series**

**Step 1: Assign the certificate to the target instance**

- Select **Assign to Instance** → choose **MetaDefender Kiosk**
- Choose your target Kiosk instance from the list, and click **Assign**.

![](https://uploads.developerhub.io/prod/97qW/07w890nfwxeinxy42rgb0odgol1t8nyk7lnx1toe9ljq763phod1idgshnu5s5sh.png)

**Step 2**: **Enable HTTPS on the instance settings**

- Navigate to **Inventory > Devices** and open the target Kiosk instance details.
- Go to the **Settings** tab, and select **Security** from the dropdown menu.
- Click **Edit**, toggle **Enable HTTPS**, choose your target certificate from the dropdown selection, and click **Save**.

![](https://uploads.developerhub.io/prod/97qW/iz0bwc88ipnfrjagg0crcv3u49sa17k0sydm4k7nkr0k89mt8pittx1ldnvxu3gb.png)

Note Only certificates listed in the instance’s **Certificates tab** are available for selection.

### **Assign to Policy**

Assigning a certificate to a policy allows you to distribute it across multiple groups of instances.

To ensure certificate is consistently applied, you need to follow **three-step process:**

1. Assign the certificate to a policy.
2. Enable HTTPS on the group settings.
3. Enable group auto-sync to ensure instances stay aligned with the group policy.

#### **MetaDefender Core**

> **Note**
>
> Assigning certificates to policies for MetaDefender Core may not function as expected in some cases. If you encounter any issues, please contact [OPSWAT Support](https://www.opswat.com/support) for assistance.

**Step 1: Assign the certificate to policy**

Select a certificate → **Assign to Policy** → choose **File Security** → choose your target policy name → click **Assign**.

![](https://uploads.developerhub.io/prod/97qW/zecr0cmq2r0jpfirak8wn6omjt3g4onnio2wo0ew2msqvbr3px6bs7ebptlnuxvw.png)

**Step 2: Enable HTTPS on the policy settings**

- Navigate to **Policies > File Security**, and open the target policy you choose in the previous step.
- In the **Settings** tab, under the **General** section, select **Security**.

![](https://uploads.developerhub.io/prod/97qW/3h189572fjkwa3wi1uo3gu3rnvmoi8b28ch19xsmf32osv8d4xqskzjmc4bj33cz.png)

- Click **Edit**, then select **Details**, toggle **Enable certificate**, select the certificate from the dropdown selection, and click **Save changes.**

![](https://uploads.developerhub.io/prod/97qW/uob37j48frbxuv25cqtpeljd8w7ojl596ub1n7bsw0pgtpyftwfdwiag34f8c2gg.png)

Note Only certificates listed in the policy's **Certificates tab** are available for selection.

**Step 3: Enable group auto-sync to ensure instances stay aligned with the group policy**

- Go to **Inventory → Groups**, click on the group using the target policy.
- In the **Settings** tab, enable **Automatically sync group policy for new instance**, then click **Save**. New instances added to this group inherit the certificate automatically.

![](https://uploads.developerhub.io/prod/97qW/smn1ahrqzr3shimqvwq53605gcg841q0s45jc9ut293zygqwms2tkx0honybym7o.png)

For **existing Core instances in the group** that do not have auto-sync enabled, you need to **turn on auto-sync** and **apply group settings** to ensure they inherit the policy and receive future updates automatically.

- Navigate to **Inventory > Services** and click on the target Core instance.
- In the **Configuration** tab, click **Apply Group Settings** to pull the policy.
- Select **Automatically sync settings from the group's policy** to pass future policy updates to this instance automatically.

![](https://uploads.developerhub.io/prod/97qW/2ne3fzp6kk7l0tqjdfn2k824ksihmrfcz5ttjijxkem2oxpcl095wg8sush90bpy.png)

#### **MetaDefender Kiosk K-Series**

**Step 1: Assign the certificate to policy**

Select a certificate → **Assign to Policy** → choose **Peripheral Media** → choose your target policy name → click **Assign**.

![](https://uploads.developerhub.io/prod/97qW/gpal5ubbsrq6julp1t359o7wg31tvotqx55xl65pitb4tw8azfnka018ghtioxgb.png)

**Step 2: Enable HTTPS on the policy settings**

- Navigate to **Policies > Peripheral Media**, and open the policy selected in the previous step.
- In the **Settings** tab, select **Security** from the dropdown menu.

![](https://uploads.developerhub.io/prod/97qW/rgdhhnd952migdomoe5ba5ag3at8ii4kwfl4jy9hdwc3mitcqc8w60swqhdqbd5g.png)

- Click **Edit**, toggle **Enable HTTPS**, select your target certificate, and click **Save**.

![](https://uploads.developerhub.io/prod/97qW/odq72eqilebgcv4xfcbfv7c6d7uwozrph71gfj4iiqpgp79etwa5upfov57ik5j1.png)

Note Only certificates listed in the policy's **Certificates tab** are available for selection.

**Step 3: Enable group auto-sync to ensure instances stay aligned with the group policy**

- Go to **Inventory → Groups**, click on the group using the target policy.
- In the **Settings** tab, enable **Automatically sync group policy for new instance**, then click **Save**. New instances added to this group inherit the certificate automatically.

![](https://uploads.developerhub.io/prod/97qW/uh3q486wdmk6lms2ft1mnrt0rjfqs4ai3ah42vgdtcfi3crk4gd78ybqu92vwy2f.png)

For **existing Kiosk instances in the group** that do not have auto-sync enabled, you need to **turn on auto-sync** and **apply group settings** to ensure they inherit the policy and receive future updates automatically.

- Navigate to **Inventory > Devices** and click on the target Kiosk instance.
- In the **Settings** tab, click **Apply Group Settings** to pull the policy.
- Select **Automatically sync settings from the group's policy** to pass future policy changes to this instance automatically.

![](https://uploads.developerhub.io/prod/97qW/sysxyzuv9vxfrf6x5a16lvw1c92yb2mlb8iak2vu2ebt3gnltt20jayzzt3hx79c.png)

## Unassign and Force Unassign a Certificate

When removing a certificate from an instance or policy, you have two options: **Unassign** and **Force Unassign**. Each option behaves differently and serves a different purpose.

#### **Unassign**

When choosing **Unassign**, My OPSWAT Central Management sends a request to the instance to remove the certificate. The status changes to **Unassigning** while in progress.

Once the instance confirms removal, the certificate is fully unassigned and removed from the list.

**How to unassign a certificate**

- Navigate to the **Certificate Details Page** and select the **Distribution** tab.
- Click the 3-dot menu and click **Unassign**.
- Confirm the action in the prompt box.

![](https://uploads.developerhub.io/prod/97qW/b9uazbti01miykw78xxzb76z188ui3ud2rf6irubyjtppplacx0yelonckyijp13.png)

#### **Force Unassign**

Force Unassign a certificate will immediately removes it from My OPSWAT Central Management without waiting for confirmation from the instance.

After a force unassign:

- The certificate may still remain on the instance.
- It is converted from a **centrally managed certificate** to a **locally managed certificate**, and will be managed directly on the product console.

![](https://uploads.developerhub.io/prod/97qW/m7xvpvj2b72lmgotwjgx9iutkn947ra0z4tqdx10ory4k0sfbe01itb3h17m2zfu.png)

Use this option when:

- The instance is unreachable or unresponsive.
- The unassign process is stuck or failed.
- Immediate removal is required.

## Deleting a Certificate

Certificates must be unassigned before deletion. If still assigned, perform **Force Unassign** first.

- Locate the certificate you want to delete.
- Click the 3-dot menu next to the certificate. Select **Delete**.
- Confirm the deletion.

![](https://uploads.developerhub.io/prod/97qW/jg42u9ca8ebtzngw2s8mcjx66lnf4d7jr08wxsrr8fnq059tw1s59p626mc4dfhk.png)

## Local Certificate

Local certificates are certificates that are imported directly on the product instance, not through My OPSWAT Central Management.

These certificates can still be viewed in the instance details, but cannot be managed from central management console.

Note This function currently applies only to **MetaDefender Kiosk (K-Series)** and is not supported for MetaDefender Core.

![](https://uploads.developerhub.io/prod/97qW/ki0024ro6fahji77hv3sxowmgx9rwi23yeowv36eu8crwz7vypbamyk6khqa7jgh.png)

**How to view local certificates**

1. Go to **Inventory → Devices.**
2. Select the target instance to open its details.
3. Navigate to the **Certificates** tab.

Local certificates are marked with an **Unmanaged** status, actions such as **assign, unassign, or delete are not available** from the central management console.

![](https:\/\/uploads.developerhub.io\/prod\/97qW\/jg42u9ca8ebtzngw2s8mcjx66lnf4d7jr08wxsrr8fnq059tw1s59p626mc4dfhk.png)
