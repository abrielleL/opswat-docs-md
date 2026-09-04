<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/misconfiguration -->

# Misconfiguration

The misconfiguration is accessible under **Policies** → **Asset Policies**→ **Misconfiguration.**

The misconfiguration page contains a list of assets with opened port policies that are not allowed to connect to the system.

Any open port that are listed in this policy will make MetaDefender OT Security trigger alerting when the asset has an unwanted port opened.

Each record in the asset list also contains additional rules about:

- The asset type/subtype or vendor.
- The open ports that the asset is not allowed, and the corresponding protocol on that port.

Misconfiguration policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

When the user acknowledge anticipated the alert, the item will display in Exception Anticipated. If the user deletes this item, MD OT Security will detect and trigger an alert related to this blocklist policy again.

## [1. View policy](/docs/md-ot-security/v.3.4.0/operating/misconfiguration#1-view-policy)

**The misconfiguration** page is paginated, each page contains *20 records*, and the total number of policy records is displayed at the bottom of the list

Policies are displayed in a list, each record contains the following information:

- ***Asset***: asset type/subtype or vendor.
- ***Protocol:*** Contains a list of allowed open ports and protocol on those ports, which is displayed in format protocol:port (e.g. http:80) where the protocol can be left blank.

## [2. Create a new policy](/docs/md-ot-security/v.3.4.0/operating/misconfiguration#2-create-a-new-policy)

You can create a new policy by tapping on the button “+” on the top right of the Policy screen, a policy creation pop-up will appear

You can check on “Highlight policies that violate in allow list”. if the current opened port rule is already in the asset allowlist, the related policy in the allowlist will be highlighted.

## [3. Edit policy](/docs/md-ot-security/v.3.4.0/operating/misconfiguration#3-edit-policy)

You can edit a policy by tapping on the “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detailed policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

Note: Field IP, MAC, and Source of the rule are non-editable.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Search policy](/docs/md-ot-security/v.3.4.0/operating/misconfiguration#4-search-policy)

The search feature for the policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields.

Click the “Clear” button to clear the values in the filters.

## [5. Remove policy](/docs/md-ot-security/v.3.4.0/operating/misconfiguration#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each policy record.
