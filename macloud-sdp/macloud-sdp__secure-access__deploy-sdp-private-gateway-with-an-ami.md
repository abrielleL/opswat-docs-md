<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/deploy-sdp-private-gateway-with-an-ami -->

# Deploy SDP Private Gateway with an AMI

This section guides you how to deploy a Private Secure IT Access Gateway with an AMI

1. Find the most recent gateway AMI for your region:

| MetaDefender IT-OT Access **Tenant** | **Available AMI** |
| --- | --- |
| Tenant B Console: console.metaaccess-b.opswat.com | - us-east-1: ami-08a74553b3041e4d7 - us-east-2: ami-0351512f7f2d56203 - us-west-1: ami-04fb409cde12c99e1 - us-west-2: ami-0b93ff9f19d27d995 |
| Tenant EU Console: console.metaaccess-eu.opswat.com | - eu-north-1: ami-0dd79548a39dc0510 |

2. Launch a new AMI. Make sure to configure the following properties:

   - The gateway instance should be at least a t2.medium (2 CPU cores and 4 GB of memory).
   - Initial configuration requires SSH access to the EC2 instance. This means giving it a public IP address, or accessing it using its private IP address from another device within the same VPC. Note that you should not enable SSH access to the gateway from any source. It’s a good idea to lock down SSH (port 22) to just those sites you want to configure the gateway from (e.g. your organization’s home office).
   - AWS will request that you provide an SSH key, and this is required in order to connect to the gateway.
   - Fill in the registration code from the MA UI in the **User data** section and set an appropriate stage. The **User data** should be formatted:`{ "accountName": "*", "stage": "*" }`. Available “stage” enumerations are `US`or `EU`The selected stage will determine which MetaDefender IT-OT Access Tenant the user connects to. You can get the registration code from the MA UI in **Settings > Global > Account**.
3. Once the AMI is available, login to the instance with SSH. The default username is ec2-user.
4. Accept and activate the gateway.

   - Login into MetaDefender IT-OT Access console.
   - Navigate to **Secure Access > Access Methods.**
   - Click **Accept** on the pending gateway, and check off **Activate the gateway** to have the gateway provisioned and ready.
