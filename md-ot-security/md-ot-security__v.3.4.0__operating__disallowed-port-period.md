<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period -->

# Disallowed Port/Period

The **Disallowed Port/Period** is accessible under **Policies** → **Connection Policies** → **Disallowed Port/Period.**

The Disallowed Port/Period contains a list of ports and communication time that are **not allowed** to establish in the system.

Any port and communication time that is listed in those policies will make MetaDefender OT Security trigger an alert when they are established in the system.

Disallowed Port/Period policies is added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

When the user acknowledges anticipated the alert, the item will display in Exception Anticipated. If the user deletes this item, MD OT Security will detect and trigger an alert related to this blocklist policy again.

## [1. View policy](/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period#1-view-policy)

**The Disallowed Port/Period page** is paginated, each page contains *20 records*, and the total number of policy records is displayed at the bottom of the list.

Policies are displayed in a list, each record contains the following information:

- ***Source device***: field source asset can have the following values:

  - Asset name in the system, detected by MetaDefender OT Security.
  - Asset type/subtype, which indicates that the policy will apply to all assets of that type/subtype.
  - Asset vendor, detected by MetaDefender OT Security.
  - Custom a specific External IP address.
  - “Any”, which indicates that the policy will apply to all assets.
- ***Destination device***: as same as the source asset.

Note: Asset type will be displayed with a green background, and “Any” will be displayed with a red background.

- ***Protocol***: Each record displays a single protocol that allows for the connection between 2 assets.

## [2. Create a new policy](/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period#2-create-a-new-policy)

You can create a new policy by tapping on the button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

## [3. Edit policy](/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period#3-edit-policy)

You can edit a policy by tapping on the “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detailed policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Filter policy](/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period#4-filter-policy)

Filter for the policy list is located at the top of the policy page,

You can search on one or more fields of the policy, just input value onto one or more fields.

If you want to search policy for a source asset with ip 192.168.1.120 and the protocol is Modbus, proceed to input “192.168.1.120” into the field source asset and “Modbus” into the field protocol, and the result list will displayed

Click the “Clear” button to clear the values in the filters.

Note: You can input the asset name or IP into the source device or destination device field, we support searching assets by both name and IP.

## [5. Remove policy](/docs/md-ot-security/v.3.4.0/operating/disallowed-port-period#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each policy record.
