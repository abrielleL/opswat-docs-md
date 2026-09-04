<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection -->

# Unauthorized Connection

The unauthorized connection is accessible under **Policies → Connection Policies → Unauthorized Connection.**

The unauthorized connection contains a list of connection policies that are **not allowed** to communicate in the system.

Any asset pair that are listed in the unauthorized connection policies will make MetaDefender OT Security trigger an alert when they have unwanted communication in the system.

Unauthorized connection policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

## [Actions on Unauthorized Connection](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#actions-on-unauthorized-connection)

## [1. View policy](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#1-view-policy)

**Unauthorized Connection page** is paginated, each page contains *20 records*, the total number of policy records are displayed at the bottom of the list.

Policies are displayed in a list, each record contains the following information:

- *Source device/Host*: field source device can have these following values:

  - Asset name in the system, detected by MetaDefender OT Security.
  - Asset type/subtype, which indicates that the policy will apply to all assets of that type/subtype.
  - Asset purdue model.
  - Asset vendor, detected by MetaDefender OT Security.
  - Custom a specific IP address.
  - “Any”, which indicates that the policy will apply to all assets.
- *Destination device/Host*: as same as source device.

Note: Asset type will be displayed with green background, “Any” will be displayed with red background.

- *Protocol*: Each record displays a single protocol that allow for the connection between 2 assets.

## [2. Create a new policy](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#2-create-a-new-policy)

You can create a new policy by tapping on button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| *Source device/Host* | Choose from drop-down list Input asset name, type, purdue model, vendor. | Choose a specific asset to apply to that asset only Choose an asset type to apply to all assets of that type Choose a vendor to apply to all assets have that vendor Choose a purdue model level to apply to all assets are on that level Choose option “Any” to apply to all assets. |
| *Destination device/Host* | Choose from drop-down list Input asset name, type, purdue model, vendor. | Choose a specific asset to apply to that asset only Choose an asset type to apply to all assets of that type Choose a vendor to apply to all assets have that vendor Choose a purdue model level to apply to all assets are on that level Choose option “Any” to apply to all assets. |
| *Protocol* | Choose from drop-down list Input protocol name (support searching by layer and protocol’s name) | Choose a specific protocol to allow only that protocol (support searching by protocol name) Left blank to allow all protocol. |
| *Enable/Disable policy option* | Tap to turn on/off policy | Once disabled, the policy will not be applied. |

## [3. Edit policy](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#3-edit-policy)

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detail policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Filter policy](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#4-filter-policy)

Filter for policy list is located at the top of the policy page,

You can search on one or more fields of the policy, just input value onto one or more fields on.

E.g. You want to search policy for a source asset with IP 192.168.1.120 and protocol is Modbus, proceed to input “192.168.1.120” into field source asset and “Modbus” into field protocol, the result list will display.

Click the “Clear” button to clear the values in the filters.

Note: You can input asset name or IP into source device or destination device field, we support searching asset by both name and IP.

## [5. Remove policy](/docs/md-ot-security/v.2.2.6/operating/unauthorized-connection#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each the policy record.
