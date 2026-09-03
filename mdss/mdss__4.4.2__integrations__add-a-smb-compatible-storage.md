<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-smb-compatible-storage -->

# Add an SMB-Compatible Storage

| Product Specification Requirements | Version |
| --- | --- |
| Service Message Block (SMB) protocol | SMB 3.1.1 (or SMB3) SMB 2.0.2 (or SMB2) |

Info

Integration with SMB Compatible Storage is currently accomplished via the Service Message Block (SMB) TCP protocol. Before you begin, you should ensure that this protocol is enabled on your computer.

In order to integrate SMB Compatible Storage with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **SMB Compatible**

2. Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later
4. **Host:** Enter the IP address of the SMB server you wish to connect to.
5. **Port**: Specify the port number used for the SMB connection, **445** being the default SMB port
6. Input the **Username** required to authenticate your access to the SMB server. (The user should have at least read and write security permissions)
7. Provide the **Password** associated with the username**.**
8. Indicate the specific directory path on the SMB server from which you want to access files .
9. Click **Continue** in order to finish the process.

Info

To avoid authentication issues the Username should have one of the following formats:

- local users should be .\username (for example: .\Administrator)
- domain users should be username@domain or domain\username
Info

A Samba file server needs to be enabled in order to connect to a Unix-based system **SharePath.** Since Samba doesn’t use the system account password, it needs to be set up using the *sudo smbpasswd -a username* command.

Info

If you use a hostname in the host portion of IPv4/v6 socket address, the program may show a non-deterministic behavior. The socket address will be resolved differently into an actual IPv4/v6 address, depending on the results from DNS resolution and/or the host configuration. For deterministic behavior use a numeric address in host portion.

Info

Windows client shares have a default configuration of 20 connections in the same time. Our default configuration will require 50 connections. To adjust this SMBSERVICE_SESSIONS_ON_STORAGE should be set to a value lower than 4

Info

Please note that SMB over QUIC is not supported at this time - only traditional SMB over TCP connections are compatible with this integration. See [[Windows] How to Expose an SMB Share as an NFS Storage Unit](/docs/mdss/4.4.2/integrations/windows-deployment--how-to-add-a-smb-share-as-a-nfs-storage-unit) for more details.
