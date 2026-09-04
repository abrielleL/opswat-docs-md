<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/deploy-a-private-gateway-with-an-ova-file -->

# Deploy a private gateway with an OVA file

This section guides you how to deploy a private gateway with an OVA file

Info

Note these are the minimum VMware Requirements for handling up to 1,000 simultaneous sessions:

- 2 CPU Cores, Reserved
- 4GB RAM, Reserved
- 10 GB Disk Space, Thick Provisioned

It is important to leverage the pooling feature and always use at least two private gateways for redundancy and availability purposes.

Note: This image is suitable for VMware environments. If you don’t have access to an enterprise VMware environment, try <https://www.vmware.com/products/workstation-player.html>.

1. Log into MetaDefender IT-OT Access console
2. Click **+ Gateway** __button at the top right to navigate to a gateway download page. Download the Private Gateway OVA file.
3. Log in as the admin user using the default password.
4. Update that default password to something more secure.
5. Give the VM a static IP address. This form will default to the IP address assigned by DHCP, but you can set it to whatever makes sense for your environment.
6. Navigate to the Register page, MetaDefender IT-OT Access will automatically register your gateway upon deployment. This step can take a while while it generates keys and calls back to Secure IT Access Controller to register itself.
7. When registration is complete you’ll be notified to go to the MetaDefender IT-OT Access console. New gateways start in a “pending” state. This means that an administrator must approve them before they can be used.
8. Navigating **Secure Access > Access Methods**, you will see the new gateway in a list of private gateways waiting to be accepted and activated. If somebody else used your registration code and you don’t recognize the entry here you could remove them instead.
9. When selecting **Accept**, a popup window will appear, you may select now to activate the gateway or activate the gateway later on in this section.
10. Test the Private Gateway connection: follow steps in [this guideline](/docs/macloud-sdp/secure-access/test-user-experience-with-a-test-app-on-a-private-gateway) to enable a testing app built-in the private gateway
