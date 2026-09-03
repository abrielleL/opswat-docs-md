<!-- source: https://www.opswat.com/docs/myop/knowledge-base/how-to-configure-the-static-ip-address-for-the-my-opswat-on-prem -->

# How to configure the static IP address for the My OPSWAT On-premises virtual appliance?

You can setup an static IP address in the [setup wizard](/docs/myop/deployment/deployment) while deploying the virtual appliance for the first time.

To configure the static IP address after the setup wizard was completed, please follow the below instructions:

1. Log into the terminal using the Local User that was created in the [setup wizard](/docs/myop/deployment/deployment).

In the My OPSWAT On-premises's virtual appliance interface (such as directly viewed through the hypervisor), you can switch to the terminal from the main interface using the hotkey combination CTRL + ALT + F3. To switch back to the main interface, use the hotkey combination CTRL + ALT + F7.

Warning

Please note that if you use SSH to log into the terminal, the SSH session will be disconnected when the IP address configuration is applied.

2. If a static IP address was previously configured in the setup wizard, run the following command to revert the IP configuration (via netplan) to the default setting, which is automatically acquiring an IP address through a DHCP server if one exists.

**sudo /os/prod-scripts/cent-netplan-default-revert.sh**

3. Use the vim utility to open (or create if it doesn't exist) the netplan configuration file 02-custom-network.yaml. Please note that this file should be located in the default working directory, i.e., /home/<local user>/bin/02-custom-network.yaml

**vim 02-custom-network.yaml**

02-custom-network.yamlCopynetwork:
version: 2
renderer: NetworkManager
ethernets:
ens192:
dhcp4: false
addresses:
- 10.40.160.99/24
routes:
- to: default
via: 10.40.160.1
nameservers:
addresses: [8.8.8.8,8.8.4.4]

Please note that the NIC name ens192 should not be changed because this is the default NIC for the virtual appliance.

You can use the **ifconfig** command to locate all NICs on the virtual appliance.

4. Modify 02-custom-network.yaml as needed and save it. Please refer to [Ubuntu's Netplan documentation](https://people.ubuntu.com/~slyon/netplan-docs/examples/) for more information.
5. Apply a new netplan configuration from 02-custom-network.yaml. Run the following command:

**sudo /os/prod-scripts/cent-netplan-apply.sh**

Netplan configuration file

Please note that the actual netplan configuration file is /etc/netplan/02-custom-network.yaml.

The file /home/<local user>/bin/02-custom-network.yaml is only a template and will have its content reset to the most up-to-date template on every upgrade.

6. If the the command completes successfully, the new static IP address configuration should take effect immediately.
