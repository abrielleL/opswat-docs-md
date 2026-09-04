<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/connection-allow-list -->

# Connection Allow List

The connection allowlist is accessible under **Policies → Connection Policies → Allowlist.**

The connection allowlist contains a list of connection policies that are allowed to communicate between assets in the system. These policies are learned during discovery phase or manual input by user. if the asset violates any rules in this connection policy, an alert will be triggered.

This page show policies that is allowed when a connection is established between the source and destination assets, including:

- Allowed protocol.
- Allowed source port.
- Allowed destination port.
- The period time allowed to communicate.
- Allowed time threshold for no connection between 2 assets. (Setting by protocol settings)

Any violation related to the policies in the allowlist will make MetaDefender OT Security trigger *alerts*.

Policies in the allowlist will be created, updated or added more detail through:

- Learning when MetaDefender OT Security is in Discovery mode.
- Manually updated by the user (**When “Anomaly Detection” is ON**).
- Automatically added when the user resolved a connection alert (Anticipated).

**In configuration page:**

- Level for alerts when having any connections violate allowlist policy. User can set level for upcoming alerts when having unrecognized connections outside the baseline if Anomaly Detections is ON.

- User can “Make alerts” or “Do not make alerts” if detection of violation of rules for time period and “Apply this setting for existing rules” or not.

- If User **select** “Make alerts“ and **check on** “Apply this setting for existing rules” checkbox, all the current policies will check on “Make alert if detection of violation of period rules above”.
- If User **select** “Make alerts“ and **uncheck on** “Apply this setting for existing rules” checkbox, all the current policies will not change the current state of “Make alert if detection of violation of period rules above”.

Info

By default: The “Do not make alerts” radio button is checked. And all the current policies and upcoming policies will not check on “Make alert if detection of violation of period rules above”.

## [Actions on Connection Allow List](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#actions-on-connection-allow-list)

## [1. View policy](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#1-view-policy)

**Connection allowlist page** is paginated, each page contains *20 records*, the total number of policy records are displayed at the bottom of the list.

Policies are displayed in a list, each record contains the following information:

- *Source asset*: field source asset can have these following values:

  - Asset name in the system, detected by MetaDefender OT Security.
  - Asset type/subtype, which indicates that the policy will apply to all assets of that type/subtype.
  - Asset vendor, detected by MetaDefender OT Security.
  - “Any”, which indicates that the policy will apply to all assets.
- *Destination asset:* as same as source asset.

Note: Asset type will be displayed with green background, “Any” will be displayed with red background.

- *Protocol*: Each record displays *a single protocol* that allow for the connection between 2 assets.
- *Source ports*: Contains a list of ports that are allowed to establish connections from these ports.
- *Destination port*: Contains a list of ports that are allowed to receive connections to these ports.
- *From*: Connection must not be available before this time.
- *To*: Connection must not be available after this time.
- *Enabled/Disabled*: Turn on/off policy.

## [2. Create a new policy](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#2-create-a-new-policy)

You can create a new policy by tapping on button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| *Source device/Host* | Choose from drop-down list Input asset name (support searching by asset's name and IP) | Choose a specific asset to apply to that asset only Choose a asset type to apply to all assets of that type Choose a vendor to apply to all assets have that vendor Choose option “Any” to apply to all asset |
| *Destination device/Host* | Choose from drop-down list Input asset name (support searching by asset's name and IP) | Choose a specific asset to apply to that asset only Choose a asset type to apply to all assets of that type Choose a vendor to apply to all assets have that vendor Choose option “Any” to apply to all assets |
| *Protocol* | Choose from drop-down list Input protocol name (support searching by layer and protocol’s name) | Choose a specific protocol to allow only that protocol (support searching by protocol name) Left blank to allow all protocol. |
| *Enable/Disable policy option* | Tap to turn on/off policy | Once disabled, the policy will not be applied when turn on anomaly detection. |
| *Alert option for inactive connection* | Check on check box to enable Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the connection violates the inactive time threshold. |
| *Criticality for inactive connection alert* | Choose from drop-down list. |  |
| *Source ports* | Input value in number format | Port numbers range from 0 to 65535 Support multi-ports input, separated by semicolon. |
| *Destination Ports* | Input value in number format | Port numbers range from 0 to 65535 Support multi-ports input, separated by semicolon. |
| *Alert option for allowed source/destination port* | Check on check box to enable Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the connection violates the allowed source/destination ports. |
| *Allowed time from* | Choose time from the clock pop-up. |  |
| *Allowed time to* | Choose time from the clock pop-up. |  |
| *Alert option for allowed time period* | Check on check box to enable Uncheck to disable. | Once unchecked, MetaDefender OT Security will not alert if the connection violates the allowed time period. |

## [3. Edit policy](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#3-edit-policy)

You can edit a policy by tapping on “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detail policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

## [4. Filter policy](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#4-filter-policy)

Filter for policy list is located at the top of the policy page.

You can search on one or more fields of the policy, just input value onto one or more fields on.

E.g. You want to search policy for a source asset with ip 192.168.1.120 and protocol is Modbus, proceed to input “192.168.1.120” into field source asset and “Modbus” into field protocol, the result list will display.

Click the “Clear” button to clear the values in the filters.

Note: You can input asset name or IP into source device or destination device field, we support searching asset by both name and IP.

## [5. Remove policy](/docs/md-ot-security/v.2.2.6/operating/connection-allow-list#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each the policy record.
