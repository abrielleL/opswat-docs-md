<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/operating/unauthorized-asset -->

# Unauthorized Asset

The unauthorized asset is accessible under **Policies** → **Asset Policies** → **Unauthorized Asset.**

The unauthorized asset page contains a list of asset policies that are not allowed to connect to the system.

*(Image could not be embedded — see Confluence)*

Any assets that are listed in the unauthorized asset policy will make MetaDefender OT Security trigger alerting when they connect to the local network.

Unauthorize asset policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

When the user acknowledge anticipated the alert, the item will display in Exception Anticipated. If the user deletes this item, MD OT Security will detect and trigger an alert related to this blocklist policy again.

*(Image could not be embedded — see Confluence)*

## [Actions on Unauthorized Asset Policies](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#actions-on-unauthorized-asset-policies)

## [1. View policy](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#1-view-policy)

**The unauthorized asset** page is paginated, each page contains *20 records*, the total number of policy records is displayed at the bottom of the list

Policies are displayed in a list, each record contains the following information:

- ***Asset***: the asset field can have the following values:

  - Asset name and IP address.
  - Asset type/subtype, which indicates that any all assets of that type/subtype is blocked when connecting to the system.
  - Vendor: which branch of asset will be blocked when MetaDefender OT Security detected.

Note: Asset type will be displayed with a green background.

- ***Criticality:*** Alert level (low/high/medium).

## [2. Create a new policy](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#2-create-a-new-policy)

*(Image could not be embedded — see Confluence)*

You can create a new policy by tapping on the button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

| **Field** | **Type of input ** | **Note ** |
| --- | --- | --- |
| ***Asset*** | Choose from drop-down listInput asset name (support searching by asset’s name and IP) |  |
| ***Enable/Disable policy option*** | Tap to turn on policy | Once disabled, the policy will not be applied. |
| ***Criticality*** | Choose from drop-down list | Alert criticality |

## [3. Edit policy](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#3-edit-policy)

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detailed policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

Note: Field IP, MAC, and Source of the rule are non-editable.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Search policy](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#4-search-policy)

The searching feature for the policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields.

Click the “Clear” button to clear the values in the filters.

Note: You can input asset name or IP into the asset field, we support searching assets by both name and IP.

## [5. Remove policy](/docs/md-ot-security/v4.0.0/operating/unauthorized-asset#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each policy record.
