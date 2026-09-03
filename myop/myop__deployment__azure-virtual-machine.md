<!-- source: https://www.opswat.com/docs/myop/deployment/azure-virtual-machine -->

# Azure Virtual Machine

You can deploy My OPSWAT on an Azure Virtual Machine using the OPSWAT plan. You can create your own virtual machine or use a pre-set configuration.

#### [Prerequisites and Requirements](https://docs.opswat.com/mdcore/cloud-deployment/single-ec2-deployment#prerequisites-and-requirements)

**Azure knowledge**: This guide assumes familiarity with Azure.

**Azure account**: needs permission to create Azure virtual machines and infrastructure and edit/create security configurations.

**DNS:** My OPSWAT uses the internal routing of the host instance and does not require any special routing.

**Scripting languages supported:** Linux - shell

Add your Subscription name, resource group and virtual machine name

StandardD4as_v4 meets the minimum resource requirement for My OPSWAT.

#### [Configure Network Settings](/docs/myop/deployment/azure-virtual-machine#configure-network-settings)

- Select the desired Virtual network you would like to deploy My OPSWAT in. My OPSWAT requires connections to the servers it manages.
- **Security groups** should follow your organizations best practices and recommendations. My OPSWAT can be used on 80 or 443 and can be changed to fit security requirements. Port 22 can be used to access via ssh for troubleshooting and administration.

#### [Configure Storage](/docs/myop/deployment/azure-virtual-machine#configure-storage)

- My OPSWAT comes with 256gb Premium SSD root volume storage

#### [Create Virtual Machine](/docs/myop/deployment/azure-virtual-machine#create-virtual-machine)

- Approximate time to initialize after launching: **~**5 minutes

#### [Sign In to My OPSWAT](/docs/myop/deployment/azure-virtual-machine#sign-in-to-my-opswat)

- Navigate to the IPv4 address or DNS of the instance you just provisioned.
- Use the default credentials admin@local / changeme12345 to login to the web management console.
