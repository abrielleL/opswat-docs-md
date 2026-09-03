<!-- source: https://www.opswat.com/docs/macloud-sdp/configuration---management/device-groups -->

# Device Groups

Within **Inventory**, administrators are able to group endpoints together and assign policies and rebranding packages. By grouping endpoints together, administrators can categorize devices and their security practices.

## [Add a Device Group](/docs/macloud-sdp/configuration---management/device-groups#add-a-device-group)

1. Go to Inventory --> Device Groups
2. Select "Create New Group".
3. Fill out the required information and choose from the available customization options for the new device group. Click on **Next** when ready.

   1. **Name, Description:** The group's name and description
   2. **Accessibility checkbox:** Choose if newly added devices should be assigned to this group automatically
   3. **Assign policy:** Assign an existing policy to the group
   4. **Assign rebranding package:** Assign an existing rebranding package to the group
4. Choose the email notification group that should be assigned under the new group. Select **Assign & Next** when ready.
5. Choose the devices that should be assigned under the new group. Click on **Create Group** when ready. Your new device group should now be displayed on the Groups management page.

## [Update a Device Group](/docs/macloud-sdp/configuration---management/device-groups#update-a-device-group)

1. From the Device Groups page, click on the group you want to update.
2. You can choose to assign a new policy or rebranding package to the group in this page (**Settings** tab).
3. Via the **Actions** drop-down menu, you can make changes to selected devices in the group. If you want to assign more devices to this group, click on **Add Devices To Group.**

## [Device Group Settings](/docs/macloud-sdp/configuration---management/device-groups#device-group-settings)

Device groups also provide administrators with the ability to override global settings set in **Settings** --> **Global**. By enabling these overrides, MetaDefender IT Access will consider the settings at the device group level above the global level settings.

- **Secure IT Access** - This override allows an administrator to enable/disable Secure IT Access.
- **Compliance Report** - This override allows an administrator to change the frequency of compliance reporting.
- **Agent** - This override allows an administrator to adjust the agent's ability to update and the agent's visibility to end-users.
- **Notification to Users** - This override allows an administrator to notify end-users about activity performed in the MetaDefender Endpoint.
- **Lost Device** - This override allows an administrator to change the frequency that MetaDefender IT Access follows for deleting lost or non-compliant devices.
