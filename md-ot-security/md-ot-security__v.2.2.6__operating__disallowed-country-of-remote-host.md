<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host -->

# Disallowed Country of Remote Host

## [Disallowed Country of Remote Host](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#disallowed-country-of-remote-host)

The Disallowed Country of Remote Host is accessible under **Policies** → **Connection Policies** → **Disallowed Country of Remote Host.**

The Disallowed Country of Remote Host contains a list of country of remote host that are **not allowed** to establish in the system.

Any remote hosts that are listed in those policies will make MetaDefender OT Security trigger an alert when they are established to that country.

Disallowed Country of Remote Host policies are added manually by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

## [Actions on Disallowed Country of Remote Host](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#actions-on-disallowed-country-of-remote-host)

## [1. View policy](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#1-view-policy)

**Disallowed Country of Remote Host page** is paginated, each page contains *20 records*, the total number of policy records are displayed at the bottom of the list.

Policies are displayed in a list, each record contains the following information:

- ***Source device/Host***: field source device can have these following values:

  - Asset name in the system, detected by MetaDefender OT Security.
  - Asset type/subtype, which indicates that the policy will apply to all assets of that type/subtype.
  - Asset vendor, detected by MetaDefender OT Security.
- ***Country***: where is the remote host that the source device/Host communicate to.

## [2. Create a new policy](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#2-create-a-new-policy)

You can create a new policy by tapping on button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| ***Internal device in the connection*** | - Choose from drop-down list. - Input asset name (support searching by asset’s name and IP) | - Choose a specific asset to apply to that asset only. - Choose an asset type to apply to all assets of that type. - Choose a vendor to apply to all assets have that vendor. |
| ***Enable/Disable policy option*** | - Tap to turn on/off policy. |  |
| ***Country of Remote Host*** | - Choose from drop-down list. |  |
| ***Alert level*** | - Choose from drop-down list. | - Alert criticality |

## [3. Edit policy](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#3-edit-policy)

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detail policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Filter policy](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#4-filter-policy)

Filter for policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields on.

E.g. You want to search policy for an **Internal device in the connection** with ip 192.168.1.120, proceed to input “192.168.1.120” into field **Internal device in the connection**, the result list will be displayed.

Click the “Clear” button to clear the values in the filters.

## [5. Remove policy](/docs/md-ot-security/v.2.2.6/operating/disallowed-country-of-remote-host#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each of the policy record.
