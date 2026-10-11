<!-- source: https://www.opswat.com/docs/mdss/4.5.2/integrations/add-a-netapp-ontap-storage -->

# Add a NetApp ONTAP Storage

NetApp ONTAP is a powerful data management software that provides unified storage for various protocols, including NFS, SMB/CIFS, iSCSI, and Fibre Channel.

It offers features like high availability, data protection, and storage efficiency, making it a popular choice for enterprise storage needs.

> **Key information:**
>
> To connect with your NetApp ONTAP storage, we rely on the Service Message Block (SMB) protocol. **Please enable SMB on your storage system beforehand for seamless integration.**

| Product Specification Requirements | Version |
| ---- | ---- |
| Service Message Block (SMB) protocol | SMB 3.1.1 (or SMB3) |
| NetApp ONTAP | 9.15.1 or later |

> **Key Information:**
>
> To use the virus scanning features (VSCAN) of your NetApp ONTAP storage with MetaDefender Storage Security **on your Windows deployment**, check out [this article](https://www.opswat.com/docs/mdss/integrations/netapp-ontap-how-to-enable-vscan) for detailed instructions.

### To integrate your NetApp ONTAP storage with this system, follow these simple steps:

1. From the left side menu, navigate to **Inventory** -> **Add** -> **Account** -> Choose **NetApp**

![](https://uploads.developerhub.io/prod/k8zL/7uo0eh4it3qczuwd30m11vxqzpoz0zevjipz3u2ic2116czp2s4uu39lyqwgu2kx.png)

3. **Provide an Account Name:** Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later

3. **Enter User Credentials**:
   1. Provide the username of an account with at least read and write permissions to the desired share.
   2. For Deep CDR & Remediations capabilities, the user needs modify permissions as well.
   3. Enter the password for the specified user.
4. Enter the IP address of the SMB server you wish to connect to.
5. Specify the port number used for the SMB connection, **445** being the default SMB port
6. Click on **Next** to finish the process.
7. From the left side menu, navigate to **Inventory** -> **Add** -> **Unit** -> Choose the previously created account

![](https://uploads.developerhub.io/prod/k8zL/tfapxi7bq4pzo614g971pzq5o829sevpjfphdr3cvh9zzwlxu14mwkj4ja0gpvx0.png)

8. Give your unit an unique name so you can easily identify it later
9. Assign your unit to a Group
10. **Specify the Share Path.** Enter the path to your network share using one of the supported formats:
    1. file://servername/pathToShare
    2. \servername\pathToShare
    3. //servername/pathToShare
    4. smb://servername/pathToShare
11. **Complete the Process:** Click **Next** to finish integrating your NetApp ONTAP storage

Once added, you can use this storage within the system for various functionalities, leveraging the capabilities of NetApp ONTAP for data management and access.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
