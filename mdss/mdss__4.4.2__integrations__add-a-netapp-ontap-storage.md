<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-netapp-ontap-storage -->

# Add a NetApp ONTAP Storage

NetApp ONTAP is a powerful data management software that provides unified storage for various protocols, including NFS, SMB/CIFS, iSCSI, and Fibre Channel.

It offers features like high availability, data protection, and storage efficiency, making it a popular choice for enterprise storage needs.

Key information:

To connect with your NetApp ONTAP storage, we rely on the Service Message Block (SMB) protocol. **Please enable SMB on your storage system beforehand for seamless integration.**

| Product Specification Requirements | Version |
| --- | --- |
| Service Message Block (SMB) protocol | SMB 3.1.1 (or SMB3) |

Key Information:

To use the virus scanning features (VSCAN) of your NetApp ONTAP storage with MetaDefender Storage Security **on your Windows deployment**, check out [this article](/docs/mdss/4.4.2/integrations/netapp-ontap-how-to-enable-vscan) for detailed instructions.

### [To integrate your NetApp ONTAP storage with this system, follow these simple steps:](/docs/mdss/4.4.2/integrations/add-a-netapp-ontap-storage#to-integrate-your-netapp-ontap-storage-with-this-system-follow-these-simple-steps)

1. From the left side menu, navigate to **Storage units.**
2. Click on **Add storage unit** and choose **NetApp ONTAP**

3. **Provide an Account Name:** Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
4. **Provide a Storage Name**: Enter a descriptive name for your storage to easily identify it later
5. **Enter User Credentials**:

   1. Provide the username of an account with at least read and write permissions to the desired share.
   2. For Deep CDR & Remediations capabilities, the user needs modify permissions as well.
   3. Enter the password for the specified user.
6. **Specify the Share Path.** Enter the path to your network share using one of the supported formats:

   1. file://servername/pathToShare
   2. \servername\pathToShare
   3. //servername/pathToShare
   4. smb://servername/pathToShare
7. **Complete the Process:** Click **Continue** to finish integrating your NetApp ONTAP storage

Once added, you can use this storage within the system for various functionalities, leveraging the capabilities of NetApp ONTAP for data management and access.
