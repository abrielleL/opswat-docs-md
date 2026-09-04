<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/supply-chain-violation -->

# Supply Chain Violation

The supply chain violation is accessible under **Policies → Asset Policies→ Supply Chain Violation.**

The supply chain violation page contains a list of assets with country of origin of NICs (COO) policies that are not allowed to connect to the system.

Any COO that are listed in this policy will make MetaDefender OT Security trigger an alert when the asset has that COO.

Each record in the asset list also contains additional rules about:

- The asset type/subtype or vendor.
- The country of origin that is not allowed.

Supply chain violation policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

## Actions on Supply Chain Violation policies

## 1. View policy

**Supply Chain** page is paginated, each page contains *20 records*, the total number of policy records is displayed at the bottom of the list.

Policies are displayed in a list; each record contains the following information:

- *Asset*: asset type/subtype or vendor.
- *COO:* country of origin of NICs.

## 2. Create a new policy

You can create a new policy by tapping on button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| Asset | Choose from drop-down list Input asset name (support searching by asset's name and IP) |  |
| *Enable/Disable policy option* | Tap to turn on policy. | Once disabled, the policy will not be applied. |
| *COO* | Choose from drop-down list Input country name. |  |
| *Criticality* | Choose from drop-down list | Alert criticality. |

Note: Create duplicate policy is not allowed.

## 3. Edit policy

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detail policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

Note: Field IP, MAC and Source of rule are non-editable.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## 4. Search policy

Searching feature for policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields.

Click the “Clear” button to clear the values in the filters.

## 5. Remove policy

You can remove a policy from the list by clicking the "Delete" button on each the policy record.
