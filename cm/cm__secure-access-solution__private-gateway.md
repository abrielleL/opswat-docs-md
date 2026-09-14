<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/private-gateway -->

# Private Gateway

## Deploy a gateway with an OVA file

This section walks you through steps to deploy a private gateway with an OVA file

> **Info**
>
> Note these are the minimum VMware Requirements for handling up to 1,000 simultaneous sessions:
>
> - 2 CPU Cores, Reserved
> - 4GB RAM, Reserved
> - 10 GB Disk Space, Thick Provisioned
>
> It is important to leverage the pooling feature and always use at least two private gateways for redundancy and availability purposes.
>
> Note: This image is suitable for VMware environments. If you don’t have access to an enterprise VMware environment, try [https://www.vmware.com/products/workstation-player.html](https://www.vmware.com/products/workstation-player.html).

1. Log into My OPSWAT Central Management console
2. Navigate to **Secure Access > Access Methods**
3. Click **Download** **Gateway** button
4. Click Download WMWare button to download the Private Gateway OVA file.
5. Import the ova to a virtual machine
6. Log in as the admin user using the default password.
7. Update that default password to something more secure.
8. Give the VM a static IP address. This form will default to the IP address assigned by DHCP, but you can set it to whatever makes sense for your environment.
9. Navigate to the Register page, My OPSWAT Central Management will automatically register your gateway upon deployment. This step can take a while while it generates keys and calls back to Secure IT Access Controller to register itself.
10. When registration is complete you’ll be notified to go to the My OPSWAT Central Management console. New gateways start in a “pending” state. This means that an administrator must approve them before they can be used.
11. Navigating **Secure Access > Access Methods**, you will see the new gateway in a list of private gateways waiting to be accepted and activated. If somebody else used your registration code and you don’t recognize the entry here you could remove them instead.
12. When selecting **Accept**, a popup window will appear, you may select to activate the gateway now or later.
13. Test the Private Gateway connection: follow steps in [Private Gateway Test Application](https://www.opswat.com/docs/cm/secure-access-solution/private-gateway-test-application) guideline to enable a testing app built-in the private gateway

## Deploy a gateway with an AMI

This section guides you how to deploy a SDP Private Gateway with an AMI

1. Find the most recent gateway AMI for your region:

| My OPSWAT Central Management **Tenant** | **Available AMI** |
| ---- | ---- |
| Tenant B Console: my.us.opswat.com | - us-east-1: ami-08a74553b3041e4d7 - us-east-2: ami-0351512f7f2d56203 - us-west-1: ami-04fb409cde12c99e1 - us-west-2: ami-0b93ff9f19d27d995 |
| Tenant EU Console: my.eu.opswat.com | - eu-north-1: ami-0dd79548a39dc0510 |

2. Launch a new AMI. Make sure to configure the following properties:
   - The gateway instance should be at least a t2.medium (2 CPU cores and 4 GB of memory).
   - Initial configuration requires SSH access to the EC2 instance. This means giving it a public IP address, or accessing it using its private IP address from another device within the same VPC. Note that you should not enable SSH access to the gateway from any source. It’s a good idea to lock down SSH (port 22) to just those sites you want to configure the gateway from (e.g. your organization’s home office).
   - AWS will request that you provide an SSH key, and this is required in order to connect to the gateway.
   - Fill in the registration code from the MA UI in the **User data** section and set an appropriate stage. The **User data** should be formatted:`{ "accountName": "*", "stage": "*" }`. Available “stage” enumerations are `US`or `EU`The selected stage will determine which My OPSWAT Central Management Tenant the user connects to. You can get the registration code from the MA UI in **Settings > Global > Account**.
3. Once the AMI is available, login to the instance with SSH. The default username is ec2-user.
4. Accept and activate the gateway.
   - Login into My OPSWAT Central Management console.
   - Navigate to **Secure Access > Access Methods.**
   - Click **Accept** on the pending gateway, and check off **Activate the gateway** to have the gateway provisioned and ready.

## Deploy a gateway with an Azure app

The OPSWAT SDP Private Gateway is an offering in the Azure marketplace that allows you to access resources hosted in Azure that you otherwise want to protect from outside access.

### Getting Started

- Starting from the marketplace, search for **OPSWAT Private Gateway** . Click **Create**.
- The pre-set configurations populate some settings for you, but probably aren’t necessary in this case. The image size is the most important factor and the default “Standard_B2s” is good enough for most workloads. We’ll customize several other options as we progress through the Azure setup in a way that the pre-set configurations don’t allow for.

### Creating the Gateway - Basics

- Select a subscription and resource group appropriate for the Secure IT Access gateway. It should be deployed in a resource group that is going to be able to get access to all protected resources that you’ll want access to, e.g. anything hosted in Azure you want to protect.
- Give it a sensible name so you can identify it later.
- Choose a region appropriate for where you’re hosting the resources. Deploying gateways to different region from what you want to protect is possible, but may introduce unneeded latency for clients as the traffic has to cross several geographic regions.
- Do not select any availability options. Secure IT Access gateways can be made highly available by deploying multiple of them, but you do not want the hosting provider to be making decisions about availability and load balancing.
- Select an appropriate size. We’ve estimated that Standard_B2s is appropriate, but your exact needs may vary depending on how much traffic you expect to put each gateway under. Deploying more gateways and allowing SDP to load balance among them is best for very large workloads.
- The administrator account is currently disabled for Secure IT Access gateways. Set up a username and password, this will be needed for you to access the gateway later when accessing it.
- Ignore the inbound port rules here, or disable it. Later on in the networking section we’ll be configuring this using a more advanced wizard to allow the right kind of traffic to reach the gateway.

### Creating the Gateway - Disks

- Here you’ll configure any additional hard disk you want attached to the VM.
- The defaults are all correct here. The image ships with the Secure IT Access gateway software pre-installed, and doesn’t require any additional disks to be mounted.

### Creating the Gateway - Networking

- Select a virtual network and subnet as appropriate. Make sure that resources you intend to protect are going to be reachable from this location. This might mean deploying the gateway to the same subnet as the resources in question, or at least making sure that network security rules on both ends allow for traffic between those subnets or virtual networks.
- Here we’re creating a new public IP for the gateway, but you can re-use one if you already have one configured. The gateway will need a public IP to allow clients to connect.

### Creating the Gateway - Networking | Network Security Group

- Select advanced configuration for the network security group, and then **Create new**.
- This VM will use more specific network security settings than the wizard permits by default with the basic option. If necessary, delete any default rules like “default-allow-ssh”.
- Select  **Create a new inbound rule**.
- The source can be from any location, and any port (“*”).
- The destination is any, from a custom port range, “30000-30001”.
- The protocol is UDP.
- The priority can be anything, as long as it’s a lower number than any existing rules. Lower numbered priorities win over higher. In the case of the SDP private gateway this should be the only rule, and this editor defaulted the form to 1010.
- Name the rule.

> **Info**
>
> While the VM can be configured without SSH access (see the “Advanced” tab), you may also enable SSH access to launch the console shell via SSH instead. In this case also create an inbound rule that enables that access. It looks similar, but destination port is 22, and the protocol is TCP.

### Creating the Gateway - Management

- Here you’ll configure extra options related to how to maintain and troubleshoot this image.
- **Disable** boot diagnostics.

> **Info**
>
> We’ve disabled boot diagnostics as it’s not required for normal functioning of the image. It is required to use the “serial console” feature that Azure provides for logging in to VMs. While we’ll be configuring the VM without this access (see the “Advanced” tab) it may be useful for troubleshooting. If this is required enable boot diagnostics.

### Creating the Gateway - Advanced

- Here you’ll configure settings related to how to deploy this image.
- For a private gateway the only part of this that will be relevant is to provide a registration code and stage to link it to your My OPSWAT Central Management account.
- Fill in the registration code from the MA UI in the **Custom data** section and set an appropriate stage. The **Custom data** should be formatted:`{ "accountName": "*", "stage": "*" }`. Available “stage” enumerations are `US`or `EU`The selected stage will determine which My OPSWAT Central Management Tenant the user connects to. You can get the registration code from the MA UI in **Settings > Global > Account**.

> **Info**
>
> The Custom data is technically optional here. If you omit it you’ll have to log in to the VM after launching it to provide this information. If you need to do this you’ll need to have previous enabled SSH access in the network security settings, or the serial console by enabling boot diagnostics.

### Creating the Gateway - Tags

- You can provide tags to help organize objects in Azure. This isn’t strictly needed, but may be useful to find all of the objects you’re creating here later.

### Creating the Gateway - Review and Create

### Deploying the Gateway

- Once the gateway is launched you should see it appear in the **Secure Access > Access Methods** area of the My OPSWAT Central Management administration console.
- If the gateway shows as provisioning with a wait icon instead of an **Accept** button just wait a few minutes. The gateway is generating cryptographic keys for securing client traffic.
- If you haven’t entered the registration code via **Custom data** in the **Advanced** tab when setting up the gateway in Azure, you will need to log in to the gateway via the Azure serial console or SSH to enter that registration code now. Once you’ve done that it should appear in the My OPSWAT Central Managements' **Access Methods** page.
- Click **Accept** next to the gateway, and a pop up window will appear. Assign to a pool and check off **Activate this gateway**.
