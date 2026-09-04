<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation -->

# Supply Chain Violation

The supply chain violation is accessible under **Policies** → **Asset Policies** → **Supply Chain Violation.**

The supply chain violation page contains a list of assets with country of origin of NICs (COO) policies that cannot connect to the system.

Any COO that are listed in this policy will make MetaDefender OT Security trigger an alert when the asset has that COO.

Each record in the asset list also contains additional rules about:

- The asset type/subtype or vendor.
- The country of origin is not allowed.

Supply chain violation policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

When the user acknowledge anticipated the alert, the item will display in Exception Anticipated. If the user deletes this item, MD OT Security will detect and trigger an alert related to this blocklist policy again.

## [1. View policy](/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation#1-view-policy)

**The Supply Chain** page is paginated, each page contains *20 records*, and the total number of policy records is displayed at the bottom of the list

Policies are displayed in a list; each record contains the following information:

- ***Asset***: asset type/subtype or vendor.
- ***COO:*** country of origin of NICs.

## [2. Create a new policy](/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation#2-create-a-new-policy)

You can create a new policy by tapping on button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

Note: Creating duplicate policies is not allowed.

## [3. Edit policy](/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation#3-edit-policy)

You can edit a policy by tapping on the “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detailed policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

Note: Field IP, MAC, and Source of the rule are non-editable.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Search policy](/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation#4-search-policy)

The searching feature for the policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields.

Click the “Clear” button to clear the values in the filters.

## [5. Remove policy](/docs/md-ot-security/v.3.4.0/operating/supply-chain-violation#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each policy record.
