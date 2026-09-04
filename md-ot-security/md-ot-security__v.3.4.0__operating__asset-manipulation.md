<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/asset-manipulation -->

# Asset Management

The asset in the system contains a lot of information:

- Asset hardware and firmware information.
- Asset connections, mini map indicating relationships with other assets, protocol pie chart.
- Asset current open port/protocol.
- Asset vulnerability. (unpatched/patched/potential)
- Asset alert and connection alert.
- Asset update history.

So this page describes how user can interact with asset in the system.

## [Import Asset](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#import-asset)

The **Bulk Import** feature allows you to efficiently add multiple assets at once by using a **CSV template**. Follow the steps below to ensure a smooth import process.

### [**Step 1: Download CSV Template**](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#step-1-download-csv-template)

Click **"Download CSV Template"** to get the preformatted file. This template ensures that your data follows the correct structure for a successful import.

### [**Step 2: Fill in Asset Details**](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#step-2-fill-in-asset-details)

1. Open the downloaded CSV file.
2. Enter asset details according to the template's format.
3. Ensure that all required fields are correctly filled.

### [**Step 3: Upload & Import**](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#step-3-upload--import)

1. Navigate to the **Import Asset** section.
2. Click **"Upload CSV"** and select the completed file.
3. The system will validate the data and process the import.

### [**Final Step: Verify Imported Assets**](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#final-step-verify-imported-assets)

- After the import is complete, review the **Asset List** to ensure all entries were added successfully.
- If any errors occur, check the CSV format and re-upload the corrected file.

## [Create Asset](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#create-asset)

Usually, asset is created automatically by MetaDefender OT Security during discovery phase. However, there is some assets MetaDefender OT Security can’t discover (Ex: access switch). In this case, user can also create new asset manually by clicking on “Create asset” button at Assets or Map page.

User can add more NICs if the asset has multiple NIC cards.

## [Edit Asset](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#edit-asset)

User can edit the asset properties even after MetaDefender OT Security completely scans. The new properties that user edited will have higher priority and will not be overridden when MetaDefender OT Security scanning the asset information again. At this time, “New properties detected**” will appear so that user can know MetaDefender OT Security has detected the new asset information. User can choose which property should be overridden.

## [Clone Asset](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#clone-asset)

This would be the same rule with creating asset.

## [Asset detail - Connection](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---connection)

You can see more detail about the asset by clicking on Detail button.

On connection tab, you can see all other assets that are connecting to the current asset on the mini map and the total connection by protocols. You can quickly open another asset by double-clicking on the node.

The connection list shows all connection that the asset has communicated.

You can sort or search any information related to the connection.

## [Asset detail - Open Port/Protocol](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---open-portprotocol)

The open port/protocol tab indicates the current open port/protocol on the asset with some information:

- Port: open/closed port.
- Protocol: protocol is using.
- Last seen open: the last time that port opens.
- Last seen close: the last time that port closes.
- Current state: current state of port.
- Possible misconfigurations: when port open but no actual traffic or violate any open port policies.
- Recheck: check possible misconfigurations.

## [Asset detail - Vulnerability](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---vulnerability)

The open port/protocol tab indicates all CVEs that the asset is being/may be unpatched.

- Unpatched: the CVEs that asset is not patched.
- Patched: the CVEs that asset have resolved.
- Potential: the CVEs that asset may not be patched.

You can see more information by click on the CVE.

- CVSS version 3.x or 2.0
- Last detected and resolved time.
- CVSS Score.
- CVE remediation document.
- Vector.

## [Asset detail - Alert](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---alert)

Alert list page includes 2 tabs: Connection alerts list and Asset alerts list.

You can click on the link for more detail.

## [Asset detail - Update History](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---update-history)

This tab indicates that what field of asset has been updated.

There are two factors that can change asset properties:

- By system, MetaDefender OT Security updates asset properties automatically during discovery/scanning.
- By administrator, user is able to update the asset information so that MetaDefender OT Security can learn and update the asset information for the next time scanning those assets.

Note: The asset changes make by administrator will have higher priority than the system.

## [Asset detail - Login History](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-detail---login-history)

This tab indicates about tracks and logs user activities for PLC Siemens

## [Asset learning mode](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#asset-learning-mode)

Action on asset learning mode:

- Extend: extend learning hours of specific asset.
- Complete: complete learning phase of asset immediately.
- User is able to force complete learning for all assets by turning on Anomaly Detection.

The asset will be put in learning mode in case:

- Before turning on Anomaly Detection, at the first time starting MetaDefender OT Security, all assets will be put in learning mode.
- After turning on Anomaly Detection, a new asset that connect to the system will be put in learning mode.
- Or user want to extend learning time.

Note: The asset and its connections will not be alerted during learning mode.

## [Field Asset](/docs/md-ot-security/v.3.4.0/operating/asset-manipulation#field-asset)

MetaDefender OT Security haven’t supported scanning field asset yet. So user need to create field assets manually.

User is able to link field assets.

to one or more controller by clicking “Link to Controller” button then click on “+” button and choose the controller that scanned by MetaDefender OT Security.
