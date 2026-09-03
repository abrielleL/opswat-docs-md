<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac -->

# Getting Started with NAC

## [Welcome aboard, and thank you for choosing NAC!](/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac#welcome-aboard-and-thank-you-for-choosing-nac)

- Download and install your VM
- Run through some initial configurations steps
- Understand how to get help and support
- Get started on your deployment
- OPTIONAL: Access training guides and other resources that might be useful

## [Download and Install Your NAC VM](/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac#download-and-install-your-nac-vm)

Please follow these instructions to download and configure the NAC VM.

1. Download the NAC image here [https://my.opswat.com/products/metaaccess-nac](https://my.opswat.com/home/metadefender-nac)

   - Note: for customers with a license for 20,000 or more users, your deployment engineer(s) will make additional configuration changes to your image after it’s installed.
2. Follow the instructions in the VM Deployment Guide to install and configure the NAC in the admin's virtual environment.

## [Initial Configuration](/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac#initial-configuration)

Info

Some of these steps may not be required for some deployments. Contact Customer Success at [opswat.com/support](https://opswat.com/support/) to get help if any of these steps are unclear. Subject: "Initial Configuration Help"

1. **DHCP syslog**

   - If you use BlueCat or another Linux-based DHCP server(s), you can usually point standard syslog output to port 514 on the NAC VM’s internal IP.
   - If you use Windows DHCP, please follow the step-by-step instructions here: [DHCP Syslog Service Installation and Configuration](https://docs.opswat.com/manac/configuration/dhcp-syslog-service-installation-and-configuration)
   - **Note:** Without DHCP syslog for all managed devices, users may need to authenticate more often than you’d like!
2. **DHCP requests**

   - For each VLAN you will manage with NAC, please add *a NEW* ip-helper statement pointed to the NAC VM’s internal IP.
   - This will be *in addition to any existing ip-helper statements.* Users will continue to get DHCP from your usual server(s), but NAC will now also see a copy of each request.
   - **Note:** Without DHCP requests, NAC will not be able to identify mobile devices or other BYOD endpoints connecting to your network!
3. **Authentication**

   - Use the following link to get NAC talking to your AD or LDAP directory server(s): [DHCP Syslog Service Installation and Configuration](https://docs.opswat.com/manac/configuration/dhcp-syslog-service-installation-and-configuration)
   - This step is critical when setting up captive portal authentication for your internal BYOD users!
   - This will also provide Single Sign On for your dot1x and secure wireless users.

Info

Contact Customer Success at [opswat.com/support](https://opswat.com/support/) to get help with any of these steps!
Subject: Network Configuration Help

1. **Set up the NAC RADIUS Server:**[RADIUS Server Configuration](https://docs.opswat.com/manac/configuration/getting-started-with-metaaccess-nac)
2. **Check out our Network Integration Guides for Layer 2 and Layer 3 enforcement**

   - [Layer 2 Integration Scripts](https://docs.opswat.com/manac/installation/layer-2-switch-controller-ap-integration-scripts)
   - [Layer 3 Integration Scripts](https://docs.opswat.com/manac/installation/layer-3-network-integration-scripts)

## [Get Your Deployment Calls Started](/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac#get-your-deployment-calls-started)

Info

Contact Customer Success at [opswat.com/support](https://opswat.com/support/) to schedule your first deployment call. Subject: Deployment Kickoff Call

## [Explore other resources](/docs/manac/nac-v8.1.1/configuration/getting-started-with-nac#explore-other-resources)

OPTIONAL: Check out our Admin and UI Guides, Troubleshooting Resources, and other helpful tools.

- The Academy NAC Pro Course on [www.opswat.com/academy](https://www.opswat.com/academy)
- [Knowledge Base, FAQ and How To Articles](https://docs.opswat.com/manac)
