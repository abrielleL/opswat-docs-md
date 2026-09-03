<!-- source: https://www.opswat.com/docs/product-management/configuration/license-management -->

# License Management

For certain OPSWAT product types, My OPSWAT provides the license management feature to help you control the licensing status of your managed instances in one place instead of having to handle each instance individually.

The supported OPSWAT product types for this feature are:

- MetaDefender Core
- MetaDefender Kiosk K-Series
- MetaDefender Kiosk L-Series
- MetaDefender ICAP Server

To access this feature, click **Licenses** in the left sidebar menu and open the corresponding tab for the OPSWAT product type, such as **MetaDefender Core.**

My OPSWAT manages the licenses differently based on their activation mode: either online or offline. Each mode has its own section in a product type's license management page.

Please note that only My OPSWAT On-premises can use the offline activation mode.

To add a license, click **Add New License.** In My OPSWAT On-premises, you will be asked to choose between [Online Activation](/docs/product-management/configuration/license-management#online-activation) or [Offline Activation](/docs/product-management/configuration/license-management#offline-activation). Please refer to the corresponding sections below to continue.

After adding a supported license to My OPSWAT, a managed product instance can contact My OPSWAT to update its own licensing status.

Priority when using both offline license and online license

If there is an offline license with a matching deployment ID available, a product instance will prefer to use that offline license instead of the online license.

### [Online Activation](/docs/product-management/configuration/license-management#online-activation)

1. To continue with online activation, enter the license key you receive from OPSWAT and click **Add.**
2. Upon success, the license management page will display your new online license with the **Active** status. Only one online license can be in-use at a time.

As noted above, when updating its license status, a product instance prefers an offline license with a matching deployment ID over the online license.

To remove the online license, click **Delete** and confirm your choice.

### [Offline Activation](/docs/product-management/configuration/license-management#offline-activation)

Please note that only My OPSWAT On-premises can use the offline activation mode.

1. To continue with offline activation, log into [My OPSWAT](my.opswat.com).
2. Click **License Management** in the left sidebar menu, and click **Activate License.**

3. In the pop-up dialog, select the corresponding product type, for example, **MetaDefender Kiosk K-Series**.

4. Enter your license key and the deployment ID of your product instance. Click **Activate.**
5. Click **Download** in the next dialog to download the activation file.

6. Go back to My OPSWAT On-premises console and upload your activation file(s).

7. You can upload multiple files with each file matching a managed instance's deployment ID. Click **Add More File** to do so.
8. Click **Add** to confirm your selection.
9. Upon success, the license management page will display your new offline license(s).

As noted above, when updating its license status, a product instance prefers an offline license with a matching deployment ID over the online license.

To remove an offline license, click **Delete License** from the corresponding entry's drop-down menu. Please note that licenses with the **In Use** status cannot be removed.
