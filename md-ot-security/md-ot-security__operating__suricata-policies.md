<!-- source: https://www.opswat.com/docs/md-ot-security/operating/suricata-policies -->

# Suricata Policies

## [What is Suricata](/docs/md-ot-security/operating/suricata-policies#what-is-suricata)

“Suricata is a high performance Network IDS, IPS and Network Security Monitoring engine. It is open source and owned by a community-run non-profit foundation, the Open Information Security Foundation ([OISF](https://oisf.net/)). Suricata is developed by the OISF.”

First, users need to select a sensor from the list at the top-right corner.

The **Suricata Policies** tab is accessible by clicking on the icon Policies in the footer menu.

**Suricata Policies** is a set of rules for connections between source and destination devices.

The **Suricata Policies** is accessible under **Policies** → **Suricata Policies**

Any asset pair that is listed in the Suricata Policies will make MetaDefender OT Security trigger an alert when they have unwanted communication violate the rules option in the system.

Suricata policies are added manually or import from rule files by the user.

Note: The blocklist policy can be detected even user didn’t turn on Anomaly Detection.

When the user acknowledge anticipated the alert, the item will display in Exception Anticipated. If the user deletes this item, MD OT Security will detect and trigger an alert related to this blocklist policy again.

## [Action on Suricata Policies](/docs/md-ot-security/operating/suricata-policies#action-on-suricata-policies)

### [1. View policy](/docs/md-ot-security/operating/suricata-policies#1-view-policy)

**The Suricata Policies page** is paginated, each page contains *20 records*, and the total number of policy records are displayed at the bottom of the list.

Policies are displayed in a list, each record contains the following information:

- ***Source asset***: field source asset can have the following values:

  - Asset name in the system, detected by MetaDefender OT Security.
  - Asset type/subtype, which indicates that the policy will apply to all assets of that type/subtype.
  - Asset purdue model.
  - Asset vendor, detected by MetaDefender OT Security.
  - Custom a specific IP address.
  - “Any”, which indicates that the policy will apply to all assets.
- ***Destination asset***: as same as source asset.

Note: Asset type will be displayed with a green background, and “Any” will be displayed with a red background.

- ***Protocol***: Each record displays a single protocol that allows for the connection between 2 assets.
- **Action:** Alert if detection of violation of rules above with the criticality
- **Criticality:** level of alert action
- **Alert message:** message of the alert
- **Rules option:** Suricata rules are used to detect network traffic that matches a specific pattern

### [2. Create a new policy](/docs/md-ot-security/operating/suricata-policies#2-create-a-new-policy)

**Add manually:** You can create a new policy by tapping on the button “+” on the top right of the Policy screen, a policy creation pop-up will appear.

**Import from rule files**: You can create a new policy by clicking on the button “Import” on the top right of the Policy screen, a policy import pop-up will appear.

Then select file has extention *.rules, example:

Example content of file we using to import:

JavascriptCopyalert modbus any any -> any 502 (msg:"Modbus TCP Read Holding Registers request"; modbus: function 3;)

| **Field** | **Type of input** | **Note** |
| --- | --- | --- |
| ***Source device/Host*** | - Choose from drop-down list - Input asset name (support searching by asset’s name and IP) | - Choose a specific asset to apply to that asset only. - Choose an asset type to apply to all assets of that type. - Choose a vendor to apply to all assets have that vendor. - Choose option “Any” to apply to all assets |
| ***Destination device/Host*** | - Choose from drop-down list - Input asset name (support searching by asset’s name and IP) | - Choose a specific asset to apply to that asset only. - Choose an asset type to apply to all assets of that type. - Choose a vendor to apply to all assets have that vendor. - Choose option “Any” to apply to all assets |
| ***Protocol*** | - Choose from drop-down list - Input protocol name (support searching by layer and protocol’s name) | - Choose a specific protocol to allow only that protocol (support searching by protocol name) - Left blank to allow all protocol |
| ***Enable/Disable policy option*** | - Tap to turn on/off policy | - Once disabled, the policy will not be applied |
| ***Action for suricata policy*** | - Select alert action from drop-down list of Action |  |
| **Criticality** ***of Action for suricata policy*** | - Select the level of action form drop-down list of Criticality |  |
| ***Source Ports*** | - Input value in number format | - Port numbers range from 0 to 65535. - Support multi-ports input, separated by semicolon. |
| ***Destination Ports*** | - Input value in number format | - Port numbers range from 0 to 65535. - Support multi-ports input, separated by semicolon. |
| ***Alert message*** | - Alert message of the alert | - The first thing to look at in a rule is the description that follows the msg keyword. Let's consider an example:   `msg:"ET SCADA [nsacyber/ELITEWOLF] Possible Siemens S7-1200 Unauthorized Access Attempt - Request for /Images/CPU1200/"` |
| **Rules option** | - Used to detect network traffic that matches a specific pattern | - These are enclosed by parenthesis and separated by semicolons. Some options have settings (such as msg), which are specified by the keyword of the option, followed by a colon, followed by the settings. Others have no settings; they are simply the keyword (such as nocase): : ; ; - Rule options have a specific ordering and changing their order would change the meaning of the rule. |

### [3. Edit policy](/docs/md-ot-security/operating/suricata-policies#3-edit-policy)

You can edit a policy by tapping on the “Edit” button on the right of each policy record, a policy editing pop-up will appear.

In the pop-up editing, you can see the detailed policy. You can edit by clicking on the field to be edited and perform input operations like when creating a policy.

When finished editing, click “Save” to save the changes or “Cancel” to discard all.

### [4. Filter policy](/docs/md-ot-security/operating/suricata-policies#4-filter-policy)

Filter for the policy list is located at the top of the policy page,

You can search on one or more fields of the policy, just input value onto one or more fields.

If you want to search policy for a source asset with ip 192.168.1.120 and the protocol is Modbus, proceed to input “192.168.1.120” into the field source asset, and “Modbus” into the field protocol, and the result list will displayed

Click the “Clear” button to clear the values in the filters.

Note: You can input the asset name or IP into the source device or destination device field, we support searching assets by both name and IP.

### [5. Remove policy](/docs/md-ot-security/operating/suricata-policies#5-remove-policy)

You can remove a policy from the list by clicking the "Delete" button on each policy record.
