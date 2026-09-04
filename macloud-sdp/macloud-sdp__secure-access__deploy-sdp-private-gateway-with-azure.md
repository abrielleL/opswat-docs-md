<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure -->

# Deploy SDP Private Gateway with Azure

The OPSWAT SDP Private Gateway is an offering in the Azure marketplace that allows you to access resources hosted in Azure that you otherwise want to protect from outside access.

## [Getting Started](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#getting-started)

- Starting from the marketplace, search for **OPSWAT Private Gateway** . Click **Create**.
- The pre-set configurations populate some settings for you, but probably aren’t necessary in this case. The image size is the most important factor and the default “Standard_B2s” is good enough for most workloads. We’ll customize several other options as we progress through the Azure setup in a way that the pre-set configurations don’t allow for.

## [Creating the Gateway - Basics](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---basics)

- Select a subscription and resource group appropriate for the Secure IT Access gateway. It should be deployed in a resource group that is going to be able to get access to all protected resources that you’ll want access to, e.g. anything hosted in Azure you want to protect.
- Give it a sensible name so you can identify it later.
- Choose a region appropriate for where you’re hosting the resources. Deploying gateways to different region from what you want to protect is possible, but may introduce unneeded latency for clients as the traffic has to cross several geographic regions.
- Do not select any availability options. Secure IT Access gateways can be made highly available by deploying multiple of them, but you do not want the hosting provider to be making decisions about availability and load balancing.
- Select an appropriate size. We’ve estimated that Standard_B2s is appropriate, but your exact needs may vary depending on how much traffic you expect to put each gateway under. Deploying more gateways and allowing SDP to load balance among them is best for very large workloads.
- The administrator account is currently disabled for Secure IT Access gateways. Set up a username and password, this will be needed for you to access the gateway later when accessing it.
- Ignore the inbound port rules here, or disable it. Later on in the networking section we’ll be configuring this using a more advanced wizard to allow the right kind of traffic to reach the gateway.

## [Creating the Gateway - Disks](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---disks)

- Here you’ll configure any additional hard disk you want attached to the VM.
- The defaults are all correct here. The image ships with the Secure IT Access gateway software pre-installed, and doesn’t require any additional disks to be mounted.

## [Creating the Gateway - Networking](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---networking)

- Select a virtual network and subnet as appropriate. Make sure that resources you intend to protect are going to be reachable from this location. This might mean deploying the gateway to the same subnet as the resources in question, or at least making sure that network security rules on both ends allow for traffic between those subnets or virtual networks.
- Here we’re creating a new public IP for the gateway, but you can re-use one if you already have one configured. The gateway will need a public IP to allow clients to connect.

## [Creating the Gateway - Networking | Network Security Group](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---networking--network-security-group)

- Select advanced configuration for the network security group, and then **Create new**.
- This VM will use more specific network security settings than the wizard permits by default with the basic option. If necessary, delete any default rules like “default-allow-ssh”.
- Select **Create a new inbound rule**.
- The source can be from any location, and any port (“*”).
- The destination is any, from a custom port range, “30000-30001”.
- The protocol is UDP.
- The priority can be anything, as long as it’s a lower number than any existing rules. Lower numbered priorities win over higher. In the case of the SDP private gateway this should be the only rule, and this editor defaulted the form to 1010.
- Name the rule.

Info

While the VM can be configured without SSH access (see the “Advanced” tab), you may also enable SSH access to launch the console shell via SSH instead. In this case also create an inbound rule that enables that access. It looks similar, but destination port is 22, and the protocol is TCP.

## [Creating the Gateway - Management](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---management)

- Here you’ll configure extra options related to how to maintain and troubleshoot this image.
- **Disable** boot diagnostics.

Info

We’ve disabled boot diagnostics as it’s not required for normal functioning of the image. It is required to use the “serial console” feature that Azure provides for logging in to VMs. While we’ll be configuring the VM without this access (see the “Advanced” tab) it may be useful for troubleshooting. If this is required enable boot diagnostics.

## [Creating the Gateway - Advanced](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---advanced)

- Here you’ll configure settings related to how to deploy this image.
- For a private gateway the only part of this that will be relevant is to provide a registration code and stage to link it to your MetaDefender IT-OT Access account.
- Fill in the registration code from the MA UI in the **Custom data** section and set an appropriate stage. The **Custom data** should be formatted:`{ "accountName": "*", "stage": "*" }`. Available “stage” enumerations are `US`or `EU`The selected stage will determine which MetaDefender IT-OT Access Tenant the user connects to. You can get the registration code from the MA UI in **Settings > Global > Account**.

Info

The Custom data is technically optional here. If you omit it you’ll have to log in to the VM after launching it to provide this information. If you need to do this you’ll need to have previous enabled SSH access in the network security settings, or the serial console by enabling boot diagnostics.

## [Creating the Gateway - Tags](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---tags)

- You can provide tags to help organize objects in Azure. This isn’t strictly needed, but may be useful to find all of the objects you’re creating here later.

## [Creating the Gateway - Review and Create](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#creating-the-gateway---review-and-create)

## [Deploying the Gateway](/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-azure#deploying-the-gateway)

- Once the gateway is launched you should see it appear in the **Secure Access > Access Methods** area of the MetaDefender IT-OT Access administration console.
- If the gateway shows as provisioning with a wait icon instead of an **Accept** button just wait a few minutes. The gateway is generating cryptographic keys for securing client traffic.
- If you haven’t entered the registration code via **Custom data** in the **Advanced** tab when setting up the gateway in Azure, you will need to log in to the gateway via the Azure serial console or SSH to enter that registration code now. Once you’ve done that it should appear in the MetaDefender IT-OT Access' **Access Methods** page.
- Click **Accept** next to the gateway, and a pop up window will appear. Assign to a pool and check off **Activate this gateway**.
