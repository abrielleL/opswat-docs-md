<!-- source: https://www.opswat.com/docs/cm/endpoint-security-solution/playbooks -->

# Playbooks

> **Info**
>
> This feature is currently in controlled release in My OPSWAT Central Management and can be available upon request. Please contact OPSWAT Support for more information.

This feature provides administrators with the ability to create conditional compliance checks that are customizable to meet all use cases for their environment. They can examine the registry, files, and more to assess compliance and security posture, a full list of capabilities is provided below. Playbooks are a visual alternative to the already existing **Custom Check** scripting capability.

## Creating A New Playbook

To create a new playbook, the administrator can navigate to **Policy Management > Playbook** and select  **Create A New Playbook**. A pop-up window will appear with the required fields - **Name**, **Description**, and **OS Type**.

After selecting **Continue**, My OPSWAT Central Management will take administrators to the **playbook editor**. In the editor, administrators can build their playbook with their desired nodes. Here in the editor, users are also able to zoom in, zoom out, and adjust the center of the playbook while building it.

- **Tasks** - This type of node includes device tasks and actions that can be added to the playbook.
- **Conditional**- This type of node includes a conditional task that will determine decisions throughout the playbook. Administrators are required to add at least one conditional node in the playbook.

To add a node to the playbook, click and drag the node onto the editor. Once added, administrators can edit the node by selecting the (**⋮**) next to the node, and choosing **Edit**. In the pop-up window, administrators can add the **Name**, **Description**, and any required fields for that specific node.

### Tasks

As mentioned above, this type of node has two sub-types: **device tasks** and **device actions**. These nodes tell My OPSWAT Central Management what to check for on a device, and then, based on conditions met, what actions to take with that device.

### Device Tasks

The current list of **device tasks** that My OPSWAT Central Management can perform, along with their descriptions (this can also be found within the playbook editor) is as follows:

- File or directory exists - Check the existence of a file or directory
- Read Windows registry - Read a value from the Windows registry
- Check Windows registry - Check the existence of a registry key or value
- Check running process - Check the running status of a process
- Get hostname - Get the hostname of a given device
- Get active username - Get the active username of a given device
- Get user domain name - Get the user domain name of a given device
- Get the list of MAC addresses - Get the list of MAC Addresses
- Check if file contains text - Check if a file contains the provided text
- Get first value of attribute - Get the first value of an attribute from an XML file
- Get all values of attribute - Get all the values of an attribute from an XML file
- Custom Script - Run a custom script on the device to create a result value to use within the playbook.

These types of task nodes can serve as your root node (the first node to start the playbook) and can continue to be used in between **conditional tasks**.

### Device Action

**Device actions** are the sub-type of this node that provide My OPSWAT Central Management with a 'response action' based on the conditional tasks and device tasks set in the playbook.

The current list of device actions that My OPSWAT Central Management can perform, along with their descriptions (this can also be found within the playbook editor), is as follows:

- Move Group - This action will move a device to another device group in My OPSWAT Central Management. There is an option to override the device group assignment. By selecting this option, any manual group assignments will be overridden.
- Set Device Status - This action will set the device's compliance status in My OPSWAT Central Management.

### Conditional Tasks

This type of node only contains one task. This task can be customized to take a output value gathered from a **device task** and then direct My OPSWAT Central Management to a specific **device action** when a device meets the condition requirement.

All conditional tasks start as an 'IF' statement, and can have additional conditions added as 'AND' statements.

The current list of conditions that My OPSWAT Central Management will check for includes:

- Empty
- Intersect
- Greater than
- Less than
- Contains
- Match
- In
- Greater than or equal
- Less than or equal
- Equal

Within the conditional task, administrators are required to fill out the **Name**, **Case Name**, **Left Value and** **Right Value** fields.

1. **Name** - Name of the conditional task
2. **Case Name** - Name of the 'IF' case
3. **Left Value** - This is the 'real' value retrieved from the device. This can either be from a task node or a fallback result. For example, the output from the 'Get Hostname' task's would become the Left Value in this conditional node.
4. **Right Value** - This is the 'desired' value that administrators want to compare to the Left Value.

Regarding **Left Value** and **Right Value**, administrators can retrieve outputs returned from task nodes by selecting **Promoted expressions** within the conditional node and selecting the desired input expression.

Another option available to administrators under **Promoted expressions** within the **Left Value** is **Check Fallbacks**. This section covers policy categories that an administrator can use to route a conditional flow down a different path in the playbook, depending on their specific use case. **Check Fallbacks** are defined in the following categories:

- Antivirus
- Hard disk encryption
- Patch management
- Threat processes
- Threats repeated

**Check Fallbacks** can be used *instead* of a task output defined earlier in the playbook. Administrators then use the description of each fallback to define the **Right Value** with their desired value to complete the conditional check. **Check Fallbacks** will always be available within a playbook and do not require a task node to become available.

For example, if an administrator wants to create a new path in the playbook for devices that have critical issues in Windows Security Center, they would input the value '2'. This is because the Windows Security Center fallback defines the values as: 0- no issue, 1 - warning, 2 - critical. Based on that conditional, the administrator can then begin the new path and continue building the playbook.

When connecting a conditional task to another device task or device action, the administrator can choose whether it follows the 'IF' statement and continues that workflow or creates the 'ELSE' branch to the 'IF' statement with an additional workflow.

### Preparing the Playbook

Before being able to save the playbook, administrators will must do the following:

- Fill out all required fields before saving the playbook.
- To create the workflow's direction, administrators must connect the nodes to one another using edges. To do this, click on any given node (⚫) and drag the arrow to the connecting node. This creates the directional flow for the playbook.
- Playbooks can only contain one root node (the first node before branching off).
- Device tasks can only be linked to another task or a condition. They cannot be linked to a device action.

Once the playbook is saved, the administrator can assign the playbook to a policy. To do so, follow these steps:

- Navigate to **Policy Management > Policies > Policy A**, with Policy A being the desired policy.
- Select the **Device Compliance** tab, and find **Playbooks**.
- Enable the **Playbooks** section, and select the desired playbook(s) to assign to the policy.
- Save.

*Note: Multiple playbooks can be assigned to a policy. If playbooks have a similar task-to-action flow,* My OPSWAT Central Management *will prioritize the first assigned playbook.*

## Playbook Example

### Scenario 1

![](https://uploads.developerhub.io/prod/97qW/th8tpbmot9sh9y18e3e2iysqiuzvaxphpf0t67sv0ovrcg57r0sjgdvi08wbk52n.png)

Check client device to see if the Notepad process is running. If Notepad is running, set the device's compliance status to COMPLIANT, else, set the device's compliance status to NON-COMPLIANT.

##

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
