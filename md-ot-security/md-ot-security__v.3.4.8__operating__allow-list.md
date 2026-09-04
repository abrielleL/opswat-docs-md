<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/operating/allow-list -->

# Allow List

The asset allowlist is accessible under **Policies → Asset** **Policies → Allowlist.**

The asset allowlist contains a list of asset policies that are allowed to connect to the system. These policies are learned during discovery phase or manual input by user. if the asset violates any rules in this policy, an alert will be triggered.

Any assets that are not listed in asset policy will cause MetaDefender OT Security consider as an “Unauthorized asset”.

Each record in the asset list also contains additional rules about:

- The time threshold that allows the asset to be inactive.
- The open ports that asset is allowed, and the corresponding protocol on that port.

Any violations of these additional rules will cause alerts to trigger as well.

Asset policies will be created or added more details for additional rules through:

- Learning when MetaDefender OT Security is in Discovery mode.
- Manually added by the user.
- Automatically added when the user resolves a asset alert with Anticipated status.

## [Asset learning period](/docs/md-ot-security/v.3.4.8/operating/allow-list#asset-learning-period)

For a new asset that connected to the system, after accepted that asset, the asset will be put in learning mode. (If user enable “inherit learning period for all assets” in wizard setup step 5)

During asset learning phase, the asset policies will be constantly updated even the Anomaly Detection is ON.

MetaDefender OT Security will stop learning the asset when learning phase is completed.

## [Actions on Asset Allowlist policies page](/docs/md-ot-security/v.3.4.8/operating/allow-list#actions-on-asset-allowlist-policies-page)

## [1. View policy](/docs/md-ot-security/v.3.4.8/operating/allow-list#1-view-policy)

**Asset** **allowlist** page is paginated, each page contains *20 records*, the total number of policy records is displayed at the bottom of the list.

Policies are displayed in a list each record contains the following information:

- Asset: Asset name and IP address.
- *Maximum inactive time*: Maximum time threshold that asset can keep inactive.
- *Protocol*: Contains a list of allowed open port and protocol on those ports, which is displayed in format protocol:port (e.g. http:80) where the protocol can be left blank
- *Enabled/Disabled*: Turn on/off policy.

## [2. Edit policy](/docs/md-ot-security/v.3.4.8/operating/allow-list#2-edit-policy)

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detail policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

You can remove a pair of allowed open ports - protocol by click on icon Delete on the corresponding row

When finished editing, click “Save” to save the changes or “Cancel” to discard all

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| Asset | Choose from drop-down list Input asset name (support searching by asset's name and IP). |  |
| *Enable/Disable policy option* | Tap to turn on/off policy. | Once disabled, the policy will not be applied when switching to Protected mode. |
| *Alert option for inactive* *asset* | Check on check box to enable. Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the asset violates the inactive time threshold. |
| *Criticality for inactive* *asset* *alert* | Choose from drop-down list. |  |
| *Time threshold for inactive* *asset* | Input value in number format. | The threshold is in seconds (s). |
| *Allowed open ports* | Input value in number format. | Port numbers range from 0 to 65535. Field “Source of rule” will display value “Manual” for any pair of open ports and protocol added by user. Otherwise displayed “Learned during discover”. |
| *Allowed protocol on corresponding ports* | Choose from drop-down list. | Allowed Protocol is an Optional field. Choose a specific protocol to allow only that protocol on that port (support searching by protocol name). Left blank to allow all protocols. |
| *Alert option for allowed open ports and protocol* | Check on check box to enable. Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the asset violates the allowed open ports and protocol |
| *Criticality for allowed open ports and protocol* | Check on check box to enable. Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the asset violates the allowed time period |

## [3. Search policy](/docs/md-ot-security/v.3.4.8/operating/allow-list#3-search-policy)

Searching feature for policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields.

E.g. You want to search policy for a Mitsubishi asset and allowed open port 44818, proceed to input

“Mitsubishi” into field asset and “44818” into field protocol, the result list will display.

Click the “Clear” button to clear the values in the filters.

Note: You can input asset name or IP into asset field, we support searching asset by both name and IP.

## [4. Remove policy](/docs/md-ot-security/v.3.4.8/operating/allow-list#4-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each the policy record.
