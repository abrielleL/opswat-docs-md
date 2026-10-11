<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/aws-fsx-for-netapp-ontap -->

# AWS FSx for NetApp ONTAP

Metadefender Storage Security is fully compatible with AWS FSx for NetApp ONTAP, leveraging NetApp's Vscan feature for seamless integration. This allows MDSS to scan files stored on your FSxN volumes for threats, helping to ensure the integrity and security of your data.

Before you begin, make sure you have:

- An operational AWS FSx for NetApp ONTAP file system.
- A Windows Server machine designated to run Metadefender Storage Security.
- Appropriate licenses for both AWS FSx for NetApp ONTAP and Metadefender Storage Security.
- Administrative access to both your AWS environment and your NetApp ONTAP configuration.

## Setup and Configuration

Follow these steps to integrate MDSS with your FSxN instance:

1. Set Up AWS FSx for NetApp ONTAP (if not already deployed)
   - Follow the official AWS documentation to create and configure your FSx for NetApp ONTAP file system:
     - AWS FSx for ONTAP Setup Guide: [Amazon FSx for NetApp ONTAP User Guide](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/what-is-fsx-ontap.html)
2. Configure Vscan for MDSS Integration
   - Vscan enables communication between your NetApp ONTAP system and external virus scanning servers, such as your MDSS instance.
   - Detailed instructions for enabling and configuring Vscan can be found in the NetApp and AWS documentation. Refer to the following resources, starting with **step 3** of the OPSWAT Vscan guide which typically outlines the ONTAP-side configuration:
     - OPSWAT Vscan Integration Guide (refer to ONTAP configuration steps): [MetaDefender Storage Security - Add A NetApp ONTAP Storage](https://www.opswat.com/docs/mdss/integrations/add-a-netapp-ontap-storage)  (This page also contains instructions for adding NetApp ONTAP as a storage unit in MDSS).
     - AWS Guide for Vscan with FSx for ONTAP: [Use NetApp ONTAP Vscan with FSx for ONTAP](https://docs.aws.amazon.com/fsx/latest/ONTAPGuide/using-vscan.html)
     - NetApp ONTAP Vscan Enablement (CLI reference): [vserver vscan enable - NetApp ONTAP CLI](https://docs.netapp.com/us-en/ontap-cli/vserver-vscan-enable.html)
3. Domain Membership - CRITICAL for proper authentication and Vscan communication
   - The Windows Server machine running Metadefender Storage Security **must** be a member of the same Active Directory domain as the AWS FSx for NetApp ONTAP SVM (Storage Virtual Machine) that you intend to scan.
4. Install and Configure Metadefender Storage Security
   - Install MDSS on your designated Windows Server.
   - During the MDSS configuration, add your FSxN SVM as a NetApp ONTAP storage unit, providing the necessary credentials and connection details as prompted by the MDSS interface. Refer to the [MetaDefender Storage Security documentation](https://www.opswat.com/docs/mdss) for specific instructions on adding storage units.

## **Troubleshooting**

If you encounter issues during or after the integration, use the following NetApp ONTAP CLI commands on your FSxN instance for diagnostics:

- `event log show` this command displays the event log, which may contain error messages related to Vscan or authentication. Filter for Vscan-related events for more targeted information.
  - Example: `event log show -message-name *vscan*`
- `vserver vscan connection-status show-all` this command shows the status of Vscan connections from the SVM to the scanning servers (your MDSS instances). This helps verify if the MDSS server is successfully connected.
- `vserver vscan show` this command displays the Vscan configuration for a specified SVM, allowing you to verify settings like active scanners and policies.

## **Additional Troubleshooting Tips**

- Make sure there are no firewall rules (either on the MDSS server, AWS Security Groups, or network ACLs) blocking the necessary Vscan communication ports between the FSxN SVM and the MDSS server. (Default Vscan port is 139/445 for SMB).
- Verify that the service account used by MDSS for Vscan has the appropriate permissions on the NetApp SVM and the shares being scanned.
- Confirm that the MDSS server and the FSxN SVM can resolve each other's hostnames via DNS.
- Make sure that the MDSS server and the FSxN instance (and domain controllers) have their time synchronized. Significant time skew can cause authentication issues.
- Check the Metadefender Storage Security logs on the Windows server for any specific error messages related to the NetApp integration.

## Performance Testing

The validation was performed using the [basic deployment](https://www.opswat.com/docs/mdss/getting-started/basic-deployment-single-instance) infrastructure model:

- **Windows Server**: 1 x MDSS instance and 1 x OPSWAT ONTAP Connector instance
- **Linux**: 1 MetaDefender Core instance

The performance metrics obtained from this configuration aligned with the specifications outlined in [our sizing guide](https://www.opswat.com/docs/mdss/getting-started/sizing-guide). The test successfully validated the expected performance parameters for this particular deployment architecture.

> **Note:** For detailed performance metrics and specific hardware recommendations, please refer to the official [sizing guide](https://www.opswat.com/docs/mdss/getting-started/sizing-guide).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
