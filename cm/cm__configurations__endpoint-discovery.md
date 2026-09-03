<!-- source: https://www.opswat.com/docs/cm/configurations/endpoint-discovery -->

# Endpoint Discovery

*Note: To enable this feature, Privacy Settings must be disabled.*

This setting lets selected MetaDefender Endpoint scan for available devices on networks. Administrators are able to gather local IP address, MAC address, and network card information for unknown devices.

## Enable Endpoint Discovery

This feature collects SSIDs, Gateway IPs, and Gateway MAC addresses of all connected networks found. **Only enable this feature if you are authorized to collect this information.**

To enable this feature, on My OPSWAT Management console

- navigate to Settings > Endpoint Discovery
- Check Enable unknown device discovery
- select devices that will perform the scan
- click Save

After enabling this feature, administrators are also given the option to check off **automatically monitor networks**.

Administrators can then view all the subnets that the device discovery feature can detect. To monitor a subnet, an administrator must toggle on the **Monitor** switch. Administrators are also able to update the alias provided for that subnet.

By selecting the settings icon for a given subnet, Administrators can set the assigned device group (any unknown device found in the subnet will be assigned to this group), and be prompted to select to either **manually** or **automatically** select a device to perform the discovery of unknown devices on the network. If there are devices that should not be used for discovery, it is suggested to utilize the **manually** option.

Once a device is selected (either automatically or manually), administrators can show or hide the Network discovery UI on the endpoint's MetaDefender Endpoint. For endpoints to see Network discovery, it is also **required** to enable the **Make** **MetaDefender Endpoint** **user interface available to end-users** setting under **Settings > Global > Device Agents**.

## Reviewing discovered devices

To view all devices discovered from the managed MetaDefender Endpoint, navigate to **Inventory > Discovered Devices**. Under this section, administrators can review all devices and their individual data (local IP, MAC address, etc.) and filter by OS type, network, group, etc.

Also from this section, administrators can perform actions such as:

- **Assign to Group** - Move a device to another device group.
- **Ignore** - This status on a device means that My OPSWAT Central Management will ignore this device in locating devices that are deemed non-compliant due to missing the MetaDefender Endpoint installed.
- **Undo Ignore** - This will undo the **Ignore** status on a device.
- **Mark as Acknowledged** - This will assign the status 'acknowledged' to a device to assist with auditing all discovered devices.
- **Mark as Newly Discovered** - This will assign the status 'newly discovered' to a device to assist with auditing all discovered devices.
- **Delete** - This will delete the device and its information from My OPSWAT Central Management.
