<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/operating/firewall -->

# Firewall

Navigate to the Firewall UI from the Active Director Single Sign-On page by clicking "AD Connector Firewall Settings". Alternatively, navigate to <https://portal.myweblogon.com:8443/manage/#/configuration/firewall> “ [portal.myweblogon.com](http://portal.myweblogon.com) ” can be replaced with the IP address of the NAC appliance or the custom hostname of the appliance, if applicable.

The Firewall user interface features the Monitoring Access and AD Connector Access tabs. The Monitoring Access tab allows admins to specify IPs and subnets allowed to send ping requests to the devices at the IPs and subnets specified. IPs are added and deleted by admins within that tab itself.

The AD Connector Access tab allows admins to grant access to the NAC appliance from the IPs the AD Connector is installed on so that the AD Connector can call in to the NAC API.

This portion of the UI is only applicable if the AD Connector is installed and configured. Otherwise, it will not function.
