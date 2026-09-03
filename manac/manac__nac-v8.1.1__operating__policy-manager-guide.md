<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/operating/policy-manager-guide -->

# Policy Manager Guide

Configuring policies and custom web messaging in NAC can easily done through the use of the Policy Manager. This guide will give an overview of the functionality available in the Policy Manager.

The purpose of this document is to provide an administrator with an overview and basic familiarity with the NAC Policy Manager. The NAC Policy Manager is the administrative interface used to configure Policy Groups in NAC. Using the Policy Manager, an Administrator can add, remove or edit policies, choose how they are enforced and create web messaging to educate end users about how they can self-remediate if they are out of compliance.

Access to the features of the NAC Policy Manager will vary depending on the read or write permissions granted to the end user from the User Administration section of the NAC Main Administrator Console.

## [Using the Policy Manager](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#using-the-policy-manager)

The Policy Manager can be reached by navigating to <https://portal.myweblogon.com:8443/manage> and selecting the "Policy Manager" menu option. The IP address of the appliance (Manager Node in a cluster) can be used in place of [portal.myweblogon.com](http://portal.myweblogon.com). In a Cluster environment, the Policy Manager will only be installed on the Manager node.

Each Policy Group consists of one Qualifier Container and one Policy Container. The Qualifier Container contains sets of qualifiers that determine which devices will be placed in a Policy Group. The Policy Container contains the policies that will be assessed on devices in a Policy Group.

## [Policy Management](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#policy-management)

The Overview tab gives a tree of what qualifiers and policies make up a policy group. The first five groups (Free Access, Open Access, Block Access, Guest Pass and Discovery) are discussed in the [SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy) section of this document.

***Whenever a change is made in the Policy Manager, click “Save” before moving to a new screen. The “Apply and Use” button will need to be clicked for changes to be live.__When clicking “Apply and Use”, a list will be presented with all the Saved changes since “Apply and Use” was last pressed. If you want to back out any of those changes, click “Cancel”.***

Info

***“Apply and Use” clears and rebuilds the server-side policy caches, an operation that can be resource intensive. As a result, it’s a good idea in general to click the button once per session, whenever possible.***

Warning

Please pay special attention to the [SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy) section's entry for Free Access. Proper use of this group can allow the NAC admin to instantly defuse many otherwise tense situations!

Because NAC is an opt-in system, networks whose IPs are not placed in a Policy Group will not be under NAC enforcement. The same applies to host types of devices.

### [Qualifiers](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#qualifiers)

Qualifiers consist of one or more criteria that describe a device or user. Qualifiers are listed in the chart below.

| Qualifier Type | Note |
| --- | --- |
| **IP Address** |  |
| **IP Range** | OPSWAT recommends specifying the DHCP Scope when using an IP Range |
| **IP Subnet** | OPSWAT recommends using IP Range over IP Subnet whenever possible |
| **Mac Address** | Received from DHCP, RADIUS accounting or a Policy Key |
| **Device Attribute** | Device Attributes can be defined for domain member Windows, macOS machines and RADIUS |
| **Username** |  |
| **User Role** | Roles can be pulled from either AD/LDAP or Guest User roles. |
| **Machine Type** | Machine Types are predefined and not user editable |

A qualifier can be added by choosing “Qualifier Menu” > “Qualifiers” and then choosing one additional sub-tab.

**Single IP**

A single IP can be added by choosing the “IP” sub-tab, entering the IP address and clicking save. Before an IP address can be enforced, a subnet mapping must be created in the configuration pages.

Info

**Best Practice:** Single IP addresses are typically used in testing, to place a small number of hand-picked devices under policy. Alternately, single IPs can be placed in the Free Access policy group (see the[SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy)section at the end) to provide exemptions for sensitive equipment with static IPs if they would otherwise match on another policy group.

Info

Qualifier names are automatically created when entering the specific criteria. For example, entering “1.1.1.1” as the IP address will automatically populate the name as “IP - 1.1.1.1”. It is recommended to keep the default Name and enter a description if more information is needed.

### [IP Range](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#ip-range)

An IP range can be added by choosing the “IP Range” sub-tab, entering the start and finish IP Address and clicking save. Before an IP Range can be enforced, a subnet mapping must be created in the configuration pages.

An IP range can be added by choosing the “IP Range” sub-tab, entering the start and finish IP Address and clicking save. Before an IP Range can be enforced, a subnet mapping must be created in the configuration pages.

Info

**Best Practice:** In general, it’s recommended to specify managed network addresses as ranges that correspond with your DHCP pools. This assures that devices with static IPs will be exempt from policy.

**IP Subnet**

An IP subnet can be added by choosing the “Subnet” sub-tab, entering the network address, choosing the mask and clicking save. Before a subnet can be enforced, a subnet mapping must be created in the configuration pages.

An IP subnet can be added by choosing the “Subnet” sub-tab, entering the network address, choosing the mask and clicking save. Before a subnet can be enforced, a subnet mapping must be created in the configuration pages.

Info

**Best Practice:** IP subnets can be used to easily specify very large subnets. Please be sure to add specific exemptions to Free Access by IP or Mac address for equipment like wireless APs.

**User Roles**

An LDAP user or Guest role can be added by choosing the “Role” sub-tab, entering the Role name and clicking save. Guest roles must first be created in the configuration pages.

**Usernames**

An individual username can be added by choosing the “User” sub-tab, entering the username and clicking save.

**MAC Address**

A MAC address can be added by choosing the “MAC Address” sub-tab, entering the mac address and clicking save.

**Device Attributes**

A Device attribute can be added by choosing the “Device Attributes” sub-tab, selecting the source, attribute name, entering the value and clicking save.

Info

Device attributes can only be used to apply policy group based on ownership information from Active Directory managed devices or location information from RADIUS accounting (Access Point or switch port. If none of these is present on the network, the device attribute cannot be used.

For Cisco Wireless, before location attributes can be used, ensure that under “Security > RADIUS > Accounting” “Acct Called Station ID Type” is set to "AP MAC Address:SSID".

Warning

When using a qualifier other than IP, the IP address and device type combination *MUST* be under policy in at least one other Policy Group before the policies you have set for that qualifier are applied. If the IP is NOT under policy somewhere, the endpoint will not be redirected to NAC. Placing the IP address in either Free Access or Open Access groups will exempt the device from policy because Free Access and Open Access have a higher priority.

This is behaving as designed to prevent devices from being blocked if they roam to subnets that should not be affected by NAC.

### [Qualifier Sets](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#qualifier-sets)

After qualifiers have been defined, qualifier sets must be created. Qualifier sets have an implied OR condition between their qualifiers. There are four qualifier archetypes, defined in the chart below:

| Qualifier Archetype | Included Qualifiers |
| --- | --- |
| **Machine Type** | OS type – values are static and not user defined |
| **Networking** | IP, IP range and IP subnet |
| **Device** | Mac Address and Device Attribute |
| **Identity** | Username and User Role |

A qualifier set includes one or more qualifiers of the same archetype.

Info

Machine types are maintained by OPSWAT. As new devices are identified, appliances will receive the new fingerprints as part of their nightly update scripts that are included as part of OPSWAT’s managed service. No action is needed to receive the latest updates.

A qualifier set can be created by choosing “Qualifier Menu” > “Qualifier Sets”. From here, click “New” and enter a name, select an archetype and the desired qualifiers. Once completed, click the save button.

Info

If many qualifiers need to be added, this can be accomplished with the Bulk Import feature. A common use case for this is a network where there are dozens of network printers to be exempted by adding their Mac Addresses to Free Access. Please see the [bulk](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-bulk) for complete instructions.

To locate an existing qualifier set, use the instant search box on the left.

### [Qualifier Containers](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#qualifier-containers)

A Qualifier container includes two or more qualifier sets. Every qualifier container must contain a single machine type qualifier set and one or more additional qualifier sets. A qualifier container can only contain one qualifier set for each of the four archetypes. Qualifier containers have an implied AND condition between their qualifier sets.

A common qualifier container could combine a host type of Windows with a network set containing an IP range, and an identity set containing the faculty LDAP role. In this use case, a user must be on a Windows device, while connected to one of the defined IP range, AND authenticated with faculty credentials to match on this container.

This specific configuration can be used to prevent internal users from accessing Guest networks, for example.

Info

If two or more containers of the same archetype are desired, a new container must be created that includes all the individual qualifiers of both sets.

A qualifier container can be created by choosing “Qualifier Menu” > “Qualifier Container”. From here, click “New” and enter a name, select no more than one qualifier set for each archetype. Once completed, click the save button.

Check one of the Archetype boxes (Machine Types, Networking, Device, Identity) to show only Sets of that type.

To locate an existing qualifier container, use the instant search box on the left.

### [Policies](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#policies)

Policies define the posture assessments to be enforced in a given policy group, and how failed assessments are enforced. The chart below gives an overview of policies and how they can be enforced.

| Policy | Requires Policy Key | Audit | Warn | Quarantine |
| --- | --- | --- | --- | --- |
| **Authentication** | **No** | **No** | **No** | Yes |
| **Policy Key** | Yes | Yes | Yes | Yes |
| **NAT Detection** | Yes | Yes | Yes | Yes |
| **Anti-Virus** | Yes | Yes | Yes | Yes |
| **OSX Update** | Yes | Yes | Yes | Yes |
| **Windows Update** | Yes | Yes | Yes | Yes |
| **End of Life** | Yes | Yes | Yes | Yes |
| **Block Access** | **No** | **No** | **No** | Yes |
| **Custom** | Yes | Yes | Yes | Yes |

Creating policies is done by selecting the sub-tab that corresponds with the policy that will be enforced:

Once the "what" has been defined, the "how" must also be defined. Enforcement actions can be an audit, warn, quarantine, or a mix of multiple warnings followed by a quarantine. This table describes each:

| Enforcement Action | Description |
| --- | --- |
| **Quarantine** | - Users failing the policy will immediately be blocked from regular network access. - Users will still have access to various remediation resources via a web proxy, including most antivirus vendor sites. - Access can often be provided to network shares and other non-port 80 resources, via modifications to one of the NAC-specific Access Control Lists (ACLs). Please email [opswat-support@opswat.com](mailto:opswat-support@opswat.com) with any questions about this feature. - Similar access can be provided for customers using Radius Based Enforcement (RBE). Please email [opswat-support@opswat.com](mailto:opswat-support@opswat.com) with any questions about this feature. |
| **Warning** | - Users are presented with a warning for being out of compliance at the specified interval. Network access is granted. |
| **Audit Only** | - Users are allowed network access. Compliance status is reported and visible in the Dashboard, but the end user is not notified or blocked. * |

Info

- **Audit Only Best Practices**: This feature should be used when compliance issues can be addressed at the convenience of end users and help desk staff.

A policy can be created by choosing “Policies Menu” > “Policies”.

When choosing an enforcement action for a policy, several common choices are available as shown in the screenshot. All policies, except for Authentication, Policy Key and Always Block allow the choice of how to enforce. A custom enforcement option is provided for cases where the common choices will not suffice for the environment. To use custom enforcement, choose the “Custom enforcement” option from the dropdown and then choose “edit”.

When using custom enforcement thresholds, up to 4 enforcement actions can be chosen. If multiple actions should be taken, all but last action must be either Temporary Warning or Temporary Quarantine. The final action can be set to any item. Temporary actions, or a recurring warning, require a duration to be set.

Each action is outlined in the table below.

| Enforcement | Definition | Configurable Duration | User will be blocked |
| --- | --- | --- | --- |
| **Temporary Warning** | End user will receive a warning message. After the duration, the client must receive an additional enforcement action. | Yes | No |
| **1-time Warning** | End user will receive one warning with no further enforcement actions. | No | No |
| **Recurring Warning** | End user will receive warning messages on a configurable duration. No further enforcement actions are permitted. | Yes | No |
| **Temporary Quarantine** | End user will be quarantined and receive a message indicating why, after the duration expires, the client must receive an additional enforcement action. | Yes | Yes |
| **Perpetual Quarantine** | End user will be quarantined and receive a warning message until compliance is met. No further enforcement actions are permitted. | No | Yes |

**Authentication**

To use authentication, choose the “Authentication” sub-tab, selecting an Authentication Scheme, selecting an Authentication web message and choosing an authentication frequency. OPSWAT recommends NAC administrators always check the “Use HTTPS for authentication” checkbox to ensure users are submitting credentials securely. Once complete, click on the “Save” button.

Info

Policy names are automatically created when entering the specific criteria just as they are when entering qualifiers. It is recommended to keep the default Name and enter a description if more information is needed.

**Authentication Best Practices:**

Authentication is often the most visible component of any NAC deployment. As such, it pays to put some thought into how often users should be required to authenticate.

Extremely frequent, or untimely, authentication can result in a frustrating end user experience. This can lead to a difficult end user relationship with Help Desk or Networking personnel. Examples of frequent authentication include:

- **Force re-authentication every X hours***–* This option is typically only recommended for Guest networks, where it is not important to allow users long periods of uninterrupted access. Frequent interruptions may even be desirable since they encourage users to move to different network segments. This option should be used with *extreme caution* on wired networks since it will likely interrupt users during an active internet session. This option should *never* be used on secure wireless.
- **Every Login** – Since users often log out and back in several times per day, forcing a manual authentication each time can be perceived as excessive.

On most production networks, it’s best to provide users with longer periods of uninterrupted access. Examples of longer authentication periods include:

- **One Time** – Prompts users for credentials when they first enter the network on a given device, then persists the correlation of username to device indefinitely, if the device accesses the network every 30 days.

  - This setting can be especially helpful on open wireless networks, where endpoints will typically pick up an IP address, even if the end user is unaware of being connected to the network. On router enforced networks, one-time authentication ensures that the NAC_Block Access List contains as few unnecessary IP addresses as possible.
- **Every Session Provided X hours have passed** – Gives users several hours, during which they can log out and back in as many times as they like, without being prompted for authentication.

  - If set to 168 hours, the user will be prompted to authenticate *at most* once per week, and *never* during an active session. This is a very popular choice for wired networks.
  - If set to 720 hours, this will allow a full 30 days between authentication prompts.
- **Force Authentication on DATE** – Fails everyone in the authentication policy on the specified date. This is commonly used in education environments where admins want to re-authenticate all users at the start of a new session or semester.

Note

Changing the Authentication Type will cause all users within the selected Authentication Policy to fail authentication and be re-assessed against the new Authentication Type that is selected.

### [NAT Policy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#nat-policy)

NAT (Network Address Translation) detection allows NAC to identify machines that are behind an unauthorized personal router. This functionality is only available to Policy Key devices. NAT Detection works by comparing the DHCP assigned upstream IP address to the local IP address of the machine as reported by the Policy Key. If the Policy Key reported local IP address does not match the DHCP assigned IP address, the machine will be flagged for failing NAT detection. To use NAT detection, choose the “NAT” sub-tab and selecting the enforcement level. Once complete, click on the “Save” button.

Note

Due to not having full visibility behind a NAT device, OPSWAT considers it a best practice to block/quarantine devices performing NAT.

In the event that blocking for NAT is not possible, the first device behind the NAT device will be elected as the controlling device and all other devices will inherit the policy and enforcement status of this new controlling device —regardless of whether the device is Policy Key-enabled or not. During a transition, a new controlling device will be selected which may potentially result in a disruption of service for other clients behind the NAT'd Device.

**AntiVirus**

NAC contains a comprehensive and up-to-date list of antivirus software for both Windows and Macintosh machines. In situations where domain managed machines require a specific antivirus package, the Policy Manager can be used to select only the approved package. For other machines that do not require a specific antivirus, select all the antivirus packages in the list.

To use anti-virus detection, choose the “Anti-Virus” sub-tab and select the anti-virus packages to check for. Alternatively, checking the “Let the system manage AV Packages” will enable all anti-virus packages by default. This option is the only way to automatically include any new AV packages that become available. Once Anti-Virus packages have been selected, a separate enforcement level must be set for Installed, Running and Definitions. Once complete, click on the “Save” button.

Info

If a user is blocked for not having any antivirus software installed, they will have access to a list of pre-approved antivirus vendor websites to self-remediate. Some antivirus vendors update their definitions via https. It is recommended in most cases to set the enforcement action for antivirus definitions to Continuously Warn in place of Immediate Quarantine. If machines are quarantined for definitions, they may not be able to self-remediate if their chosen antivirus vendor updates their definitions via https.

**Windows Update**

When a Windows Update patch policy is in place, if a user has Windows Update set to download and install, they will always pass the OS update policy regardless of how strict the requirements are configured. To use patch settings detection, choose the “Windows Update” sub-tab and selecting the patch policy and enforcement level. Once complete, click on the “Save” button.

If an on-site WSUS server should be used, select “WSUS Server” from the Patch Policy dropdown. A box will appear where a registry key can be placed. The registry key can be obtained from any machine that is already configured to use the WSUS server. From regedit, export the registry key below, then copy and paste its contents:

HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows\WindowsUpdate

*_End of Life *_Policy

When an End of Life policy is in place, devices with the major OS version designated will fail policy. To use patch settings detection, choose the “End of Life” sub-tab and select the OS versions to mark to treat as End of Life along with the enforcement level. Once complete, click on the “Save” button.

**Block Access**

The *Block Access* policy is useful for creating catch groups where users will not be allowed access until they have authenticated. After authentication, they will move to another policy group based on their end user role. To use an always block policy, choose the “Block” sub-tab and select the web message from the dropdown. Once complete, enter a name and click on the “Save” button.

Block access policies should only be used in situations where a remediation path is available, and an appropriate remediation page is going to be displayed to blocked users. NAC is not intended as a solution to block unwanted users in masse but to ensure that users are in compliance with an organization’s AUP. The two most common scenarios where a block access policy can be used are as follows:

- **WPA2 Enterprise On-Ramping** – When using WPA2 enterprise wireless, there is often a need to have an open SSID with instructions directing the end user to set up their system for WPA2 enterprise. The block policy will have a custom block message containing the on-ramping instructions.
- **Device Enrollment** – Gaming and media devices will be placed in a device blocking policy group upon accessing the network. This Policy Group will use IP as the qualifier. As users register their devices, they will be moved to another Policy Group specifically for enrolled devices.

Warning

When using router enforcement, the Block access policy is not an effective method for black-holing entire device classes as it can cause significantly higher router load and will result in a negative end-user experience for all network users.

Custom policies can also be edited from the “Custom” sub-tab. Custom policies will be covered in more detail in the Custom Policies Deep Dive section of this document.

### [Policy Containers](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#policy-containers)

A Policy container includes one or more policies. In general, a policy container should not contain more than one of each policy type (for example, Authentication, Policy Key, Antivirus, NAT or Windows Updates) except for custom policies. A Policy container can have any number of custom policies.

When building a policy container, policies will be assessed in the order they appear on the selected side. Because of this, policies that block should be placed highest in the list, followed by warning policies and ending with audit only policies.

A policy container can be created by choosing “Policies Menu” > “Policies Container”. From here, click “New” enter a name and select one or more policies. When the container is built, click the “Save” button.

### [Policy Groups](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#policy-groups)

A Policy Group contains one Qualifier Container and one Policy Container. To create a Policy Group, choose the “Group” tab, enter a name and choose both a Qualifier Container and a Policy Container. When the group is built, click the “Save” button.

Five Policy Groups are reserved for system use. These policy groups are described in more detail in the [SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy) section of this document.

Note

Special attention should be given to the [SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy) sections on **Free Access**. This can be the most useful policy group in NAC and can be especially useful when troubleshooting or dealing with unexpected interruptions of service.

### [Group Priority](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#group-priority)

When creating policy groups with overlapping qualifiers, the group priority matters. If a device matches the qualifiers of multiple groups, it will always be placed in whichever group has the highest priority. In production scenarios, it is common for one policy group to have machine type, IP and role qualifiers and a second policy group with machine type and IP qualifiers. Because the first policy group is more specific, it should have a higher priority. For this reason, groups with 3 or more qualifier archetypes, should generally be given a higher priority than groups with only 2 qualifier archetypes. Likewise, groups with a very specific set of qualifiers should also be given higher priority than a group with less specific qualifiers.

Info

By default, Free Access always has the highest priority, followed by Open Access, Block Access, Guest Pass and Detection respectively. The priority of the first five policy groups is static and cannot be changed. User-created policy groups will always have a lower priority than these four groups.

The Free Access group specifically, can be extremely useful in production. It provides the flexibility to easily mitigate or defuse potentially troublesome issues with a few keystrokes. This group is covered in more detail in the [SpecialPurposePolicy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#src-4084964_PolicyManagerGuide-SpecialPurposePolicy) section, including specific use cases.

## [Custom Policies Deep Dive](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-policies-deep-dive)

In general, creating custom policies should follow this workflow:

## [Custom Messaging](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-messaging)

Custom Messaging allows an administrator to edit what is displayed to the end users when they are redirected by NAC. To access Custom Messaging, click on “Web UI Menu" > "Web Messages” tab in the Policy Manager.

A list of all existing web messages will appear on the left. Each page will correspond with a policy. For example, if a user is failing for Symantec antivirus not running, there is a page specifically for Symantec antivirus not running. For each web message, there are separate sections that can be displayed based on whether the policy is set to warn or quarantine.

When viewing the list of web messages, choosing the “Standard” or “Custom” radio buttons will make it easier to differentiate which messages are part of NAC by default and which are completely custom. Standard messages can still be edited, but they will always appear as a standard message.

A list of all existing web messages will appear on the left. Each page will correspond with a policy. For example, if a user is failing for Symantec antivirus not running, there is a page specifically for Symantec antivirus not running. For each web message, there are separate sections that can be displayed based on whether the policy is set to warn or quarantine.

When viewing the list of web messages, choosing the “Standard” or “Custom” radio buttons will make it easier to differentiate which messages are part of NAC by default and which are completely custom. Standard messages can still be edited, but they will always appear as a standard message.

Previewing a web message will display what end users will see when they are out of policy. Before clicking on “Preview Web Message” ensure that the correct radio button is selected based on whether the quarantine or warning message should be previewed.

Warning

DO NOT attempt to use a different stylesheet without proper experience with CSS!

## [Edit a Web Message](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#edit-a-web-message)

Once a message is selected, clicking the “Download Web Message Button” will download a copy of the raw file to your local machine.

Warning

When making edits to the standard web messages, always ensure that adequate backups are being made so that it will be possible to revert to earlier revisions of the web messages. OPSWAT considers it a best practice to keep local backups of these files in addition to the nightly backups that are part of OPSWAT’s managed service.

All web messages require some basic information, but not all web messages will use a warning message and a quarantine message.

Pages that do not need a warning message:

- Authentication pages
- Pages used with custom block policies

Pages that do not need a quarantine message:

- Any page associated with a policy that will never block users

It is recommended that any page with a warning message also have a block message. This will ensure that if it is decided to enforce a policy later, the block message will be informative if the messaging is not edited.

Info

NAC Web messages are served by a java web server and support standard HTML, CSS and JavaScript as well as JSP tags for added functionality. More advanced users that wish to have direct access to the web directories to upload and edit custom CSS files, images or any other web file for use with NAC web messaging can request this access by contacting the OPSWAT Support Team.

When editing a web message, there are 4 div tags in the html page that are used to determine how the message is displayed. The Title and General sections will be displayed on both Warning and Quarantine pages. The Warning and Quarantine tags will only be displayed with the corresponding enforcement action.

- **Warning**

<div style="<c:out value="${model.warningDisplay}" />" id="warning">

Html or plain text that is found within this div tag and the closing div tag will be displayed as part of the warning message.

- **Quarantine**

<div style="<c:out value="${model.quarantineDisplay}" />" id="quarantine">

Html or plain text that is found within this div tag and the closing div tag will be displayed as part of the quarantine message.

- **Remediation Steps**

<ol class="circles-list">

This tag lists the remediation steps in order.

Once all desired edits are made to a web message, the new web message can be previewed by browsing to the file from the Web Interface and clicking the “Upload and Preview Web Message” button. After all edits have been made and the web message has been previewed, the file can be saved by clicking “Upload and Save Web Message” followed by clicking the “Save” button.

When finished editing web messaging, click on the “Apply and Use” button to save all changes to the NAC appliance.

### [Creating Remediation Steps](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#creating-remediation-steps)

When creating remediation steps, items will be listed with numbers if they are in the proper format. If numbers are preferred, steps should be listed between <li></li> html tags.

If numbers are not needed, no additional html tags should be used. Special attention should be used if sections are repeated multiple times. For messages like this, javascript is likely being used. For help on editing these messages, please consult your organization’s web team or contact OPSWAT support at [opswat-support@opswat.com](mailto:opswat-support@opswat.com).

Antivirus web messages include a generic list of options users can install. These pages should be updated to include preferred Antivirus packages.

### [Create a New Web Message](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#create-a-new-web-message)

To create a copy of an existing page, select the page from the list and click the “Copy to new Web Message” button. This will use the existing page as a template for the new page.

To create a new blank page, click the “New” button. This will create a generic page with basic information as a guide for the new message.

Info

New pages will need to be created for each custom policy.

When finished editing web messaging, click on the “Apply and Use” button to save all changes to the NAC appliance.

## [Custom Policies](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-policies)

Custom Policies allow an administrator to create a new policy to check for a specific condition on an end user machine. Custom Policies will require the Policy Key to be installed and are therefore only compatible with Windows and Macintosh machines. To access the Custom Policies settings, click on “Policies Menu" > "Policies" > "Custom” in the Policy Manager.

### [Custom Policies Options](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-policies-options)

Custom Policies are configured to check for a specific condition based on the following list:

| Condition | Windows | Macintosh | Description |
| --- | --- | --- | --- |
| Process | X | X | Checks for Running Process |
| Service Scan | X |  | Checks for a Service by name |
| Registry Key | X |  | Checks for a registry entry |
| File Search | X | X | Checks for the presence of a specific file |
| Version Check | X |  | Checks for the version of a file |
| DNS Check | X | X | Checks for approved DNS IP addresses |
| MITM Check | X | X | Checks for approved Gateway IP address |

*Process*, *Service Scan*, *Registry Key* and *File Search* can be mixed and matched in a single policy. *Version Check*, *DNS Check* and *MITM Check* should only be used in their own policy. *Always Fail* policies will cause all users in a Policy Group to be blocked.

When creating custom policy conditions, if there is no condition for a given OS, machines with that OS will not be assessed for compliance with the custom policy. For example, when looking for registry key conditions only when only the Windows XP box is checked, Windows Vista, Windows 7 and Windows 8 machines will not be assessed. Similarly, configuring a policy to only look for conditions on Macintosh machines will cause the policy to not assess Windows machines.

The Relationships between Conditions section will be set based on whether a condition is required for network access, or a condition will cause a user to be out of compliance and consequentially be warned or quarantined from network access. Custom Policies can be set to pass or fail based on a single condition, or all conditions being met.

### [Exporting and Importing a Custom Policy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#exporting-and-importing-a-custom-policy)

NAC has the ability to import/export custom policies right from the custom policy builder. Exported policies are XML formatted files and provide an easy way for OPSWAT to distribute custom policies to customers, or for customers to exchange or archive custom policies.

To export a custom policy, first, select the policy from the left panel and then click the “Export” button. At this point, you will be prompted for the location to save the resulting XML file.

To import a custom policy, click on the “Import” button and locate the XML file to be imported. Once the file is selected, click the “Upload” button and the imported policy will be created in the custom policy builder. After importing a policy, a web message and enforcement level will need to be selected.

### [Creating a New Custom Policy](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#creating-a-new-custom-policy)

To create a new policy, click on the “New” button. This example will create a policy to check for the Windows firewall running.

Enter and name and optionally enter a description. From this point, what makes up a custom policy will vary.

### [Custom Peer to Peer Sharing](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-peer-to-peer-sharing)

By default, NAC includes a custom policy that watches for a small number of peer to peer applications. A peer to peer policy is useful for presenting users with legal download alternatives, educating users about the risks of file sharing, tracking P2P usage or blocking users from using unauthorized P2P software. The included P2P policy can be edited to add or remove programs as new file sharing applications are discovered, or based on the organization’s requirements. To access this custom policy, choose “Peer to Peer Sharing Programs” from the Custom Policies drop-down menu. In this example, multiple BitTorrent clients will be added. Click on the “Add Process” button.

In this example, we will not look for an exact match. Any process with “torrent” in the name will match the policy. Click “OK” when done. Click “Save” to save changes.

The process condition will look in the “Processes” tab of the Windows task manager or the “Activity Monitor” and “ps” command on Macintosh machines. When adding items and NOT selecting the “Exact Match” checkbox, it is important to understand that any process containing the string will trigger a match. For example, if there is a desire to check for users running “The Onion Router”, looking for “tor” will trigger a match against any process with “tor” in the name including “monitor”. Entering “tor.exe” with the “Exact Match” box checked would be the proper way to check for “The Onion Router”.

Info

Mac process names are case sensitive. Window process names are not.

When the peer to peer policy is in use, a user that is quarantined can simply turn off their peer to peer software to regain network access.

### [Custom File Search](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-file-search)

One possible use case for file searches is with domain machines that need to have updated startup scripts. By checking for the presence of a specific startup file, an administrator can determine which domain machines need to be updated. Using this kind of policy, end users can be messaged to contact the IT department to get the latest updates.

After creating a new custom policy, choose all the Windows versions from the “Applied Operating Systems” Section.

Click on the “Add File Search” button.

The “File Name” field may or may not need to include a directory based on what “File Path” is chosen. Setting a “Seconds before failing the policy” value will wait the specified number of seconds before returning a fail. Click “OK” when done.

**File Path Options:**

| OS | Path Option | Equivalent File Path(s) |
| --- | --- | --- |
| Windows | All Users Profile | Users directory (“c:\Users<username>” or “c:\Documents and Settings<username>”) |
| Windows | Program Files | “c:\Program Files” and “c:\Program Files (x86)” |
| Windows | System Drive | “c:\” |
| Windows | Windows Root | must specify the full path including drive letter |
| Windows | Windows system32 | “c:\Windows\System32" |
| Mac OS X | Absolute | must specify the full path |
| Mac OS X | User Home | /Users/<username> |

Info

The above examples assume “c:” is the Windows system drive. If “c:” is not the system drive, substitute with the correct letter.

Choose the option “If ANY Conditions are met, the policy passes” and then click the “Close button”.

Choose a web message, followed by an enforcement level. When the Custom Policy is completely configured, click the “Save” button. This policy is now ready to be added to a Policy Container. When finished, remember to click on the “Apply and Use” button to save the new policy settings to the NAC appliance.

### [Custom Internet Explorer Version Check](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-internet-explorer-version-check)

After creating a new custom policy choose all the Windows versions from the “Applied Operating Systems” Section.

Click on the “Add Version Check” button.

Version checks have two options:

- **App Search**: Looks for the version of a program that is associated with the given file type (such as .pdf or .doc). The "Program name substring" field should include the name of the program used to open the files with the designated extension.
- **File Search**: Looks for the version of a specified file, such as an .exe file. This check will examine the specific file that is specified.

The Internet Explorer check will use the file search option. The app search option would be more applicable when looking for minimum PDF reader version for multiple PDF applications such as Adobe Reader and Foxit reader.

For the version numbers, the “From” field should contain the minimum allowed version. The “To” field should be a high version number that does not exist yet. This will prevent the need to constantly update the custom policy. In cases where a specific program version is required, both fields should contain the same value. Click “OK” when done.

Choose the option “If ANY Conditions are met, the policy passes” and then click the “Close" button.

Choose a web message, followed by an enforcement level. When the Custom Policy is completely configured, click the “Save” button. This policy is now ready to be added to a Policy Container. When finished, remember to click on the “Apply and Use” button to save the new policy settings to the NAC appliance.

### [Custom DNS Check](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-dns-check)

After creating a new custom policy choose all the “All PK Enabled Devices” option from the “Applied Operating Systems” Section. For DNS checks, it is recommended to always select “All PK Enabled Devices”.

Click on the “Add DNS Check” button.

Enter the IP address(es) of the DNS servers to check for and then click “OK”.

Choose the option “If ANY Conditions are met, the policy passes” and then click the “Close" button.

Choose a web message, followed by an enforcement level. When the Custom Policy is completely configured, click the “Save” button. This policy is now ready to be added to a Policy Container. When finished, remember to click on the “Apply and Use” button to save the new policy settings to the NAC appliance.

Info

A Custom DNS policy can be created to check for known rogue DNS servers. In this case, a separate rogue DNS policy would need to be created and the conditions would need to be set to “If ANY Condition is met, the policy will fail”.

### [Custom Man-in-the-Middle Check](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#custom-man-in-the-middle-check)

After creating a new custom policy choose all the “All PK Enabled Devices” option from the “Applied Operating Systems” section. For MITM checks, it is recommended to always select “All PK Enabled Devices”.

Click on the “Add MITM Check” button.

Enter the MAC addresses for any valid gateway devices on the network.

Choose the option “If ANY Conditions are met, the policy passes” and then click the “Close button”.

Choose a web message, followed by an enforcement level. When the Custom Policy is completely configured, click the “Save” button. This policy is now ready to be added to a Policy Container. When finished, remember to click on the “Apply and Use” button to save the new policy settings to the NAC appliance.

## [Special Purpose Policy Groups](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#special-purpose-policy-groups)

NAC includes 5 special purpose policy groups with special functions based on how the application is used.

- **Free Access** – Any devices on the network that should always have unrestricted access should be added to this group. Despite the name, this Policy group will accept any qualifier type, not just IP. It is important to remember that because NAC is an opt-in system, devices ONLY need to be entered FREE access if their IP is under policy somewhere. All qualifiers in this policy group are ‘OR’ conditions. To add existing qualifiers to Free Access, navigate to "Qualifiers" > "Qualifier Sets" and search for “Free Access”. Choose the qualifier set that matches the qualifier types that will be added and select the new qualifiers. Additionally, qualifiers can be added using the bulk import feature.

**Use cases:**

- **Symptom**: Large number of users unable to access the network.

  - **Cause:** When defining a large wireless subnet for policy, the controllers and APs are accidentally included in the qualifier container. The APs and controllers are blocked for identification since they don’t provide browser strings that NAC can identify. Users cannot connect to the network gear while it remains blocked.
  - **Fix:** Manually add the IP addresses, or Bulk load the mac addresses, of all APs and wireless controllers into the Free Access group. NAC immediately unblocks the controllers and APs, allowing end users to connect to the wireless network.
- **Symptom**: Large number of users unable to access the network.

  - **Cause :** Widespread policy failure. Examples:

    - **Anti-virus:** The institution’s central AV server is unable to refresh its definitions from the cloud for an extended period. As a result, all managed endpoints fail the compliance checks for up to date definitions.
    - **Authentication:** Problems with DNS or with the directory server’s LDAP database, cause NAC captive portal authentications to take much longer than expected.
  - **Fix**: In the event of a widespread policy failure, the affected network segments can be placed in Free Access. This allows users to continue accessing the network as usual until issues are surfaced and remediated.
- **Open Access** – This group should be ignored in the Policy Manager. Devices that are placed in Open Access through the Dashboard will be moved to this Policy Group and will have unrestricted access to the network. *(Please refer to the Dashboard Manual for more information on this feature).*
- **Block Access** – This group should be ignored in the Policy Manager. Devices that are placed in Block Access through the Dashboard will be moved to this Policy Group and will have their network access restricted. *(Please refer to the Dashboard Manual for more information on this feature).*
- **Temporary Access –** If using the Temporary Access feature, users will be placed in this group for the configured time of Temporary Access. Once that time expires, the users will be moved back to their standard Group.
- **Discovery***–* This group is a used for devices that have joined the network, but their device type is not yet known. The Discovery group will contain all IP address qualifiers and the detection device type. This group can be moved based on your policy requirements. Please contact OPSWAT Support if you would like more information.

## [Bulk Importing](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#bulk-importing)

The bulk importing feature is useful for creating multiple qualifiers all at once. Bulk Importing can be accessed by navigating to "Qualifiers Menu" > "Qualifier Set" in the Policy Manager.

Once in the Qualifier Set screen, choose an existing qualifier set from the list to enable the "Bulk Import" button.

After clicking the "Bulk Import" button, a dialog will open. A template can be downloaded by click on the “Download Template” button. This will download an excel spreadsheet that can be edited and uploaded to create new qualifiers.

For each qualifier, an example is given at the top of the page. Edit the template starting at line 19. Any edits made to line 19 or above will not be recognized by the system. New qualifiers must be added in the format listed in the examples in the spreadsheet. Examples are also listed in this chart:

| Valid Types (mandatory) | Qualifier Name (mandatory) | Qualifier Description (optional) | Type Data (1) (mandatory) | Type Data (2) (mandatory*) | Type Data (3) (mandatory**) |
| --- | --- | --- | --- | --- | --- |
| IP | Sample IP |  | 10.10.10.10 |  |  |
| Range | Sample IP Range |  | 10.10.10.10 | 10.10.10.254 |  |
| Subnet | Sample IP Subnet |  | 10.10.10.0 | 255.255.255.0 |  |
| Username | Sample Username |  | JDoe |  |  |
| Role | Sample Identity Role |  | Students |  |  |
| Mac | Sample Mac Address |  | AA:BB:CC:DD:EE:FF |  |  |
| Attrib | Sample Device Attribute |  | LDAP | Domain | Corporate |

Info

_The “*Type Data (2)*” field is _*only** mandatory when importing the IP ranges and subnets, or when importing the Domain device attribute. When using the Domain attribute, please **do not** fill in the “*Type Data (1)*” or “Type Data (3)” columns.

Info

** The *“Type Data (3)”* field is **only** mandatory when specifying the Corporate or Personal Liability attribute. When using the Liability attribute, please **do not** fill in the *“Type Data (1)”* or *“Type Data (2)”* columns.

Once all changes have been saved to the spreadsheet, choose the “Browse” button from the Bulk Import dialog and select the saved spreadsheet. Then click the “Upload” button. Imported qualifiers will be displayed in the results box. Any errors will also be displayed.

Info

Bulk importing does not automatically add qualifiers to a qualifier set. After a bulk import is completed, any newly created qualifiers will need to be added to the desired qualifier set.

## [Worksheets](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#worksheets)

Policies to Enforce Worksheet

| **Policy** | **Target Population** | **Machine Types** | **Enforcement Action** | **Messaging Complete** | **Notes** |
| --- | --- | --- | --- | --- | --- |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |
|  |  |  |  |  |  |

Policy Groups Worksheet

| **Policy Group Name** | **Target Population** | **Machine Type** | **Group Qualifier** | **Notes** |
| --- | --- | --- | --- | --- |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |
|  |  |  |  |  |

## [Related Content](/docs/manac/nac-v8.1.1/operating/policy-manager-guide#related-content)

- [Design Options](/docs/manac/nac-v8.1.1/operating/design-options)
