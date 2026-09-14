<!-- source: https://www.opswat.com/docs/mdss/integrations/add-an-smb-compatible-unit-in-windows-deployments -->

# Add an SMB-Compatible unit in Windows deployments

This article is **applicable only for MetaDefender Storage Security** deployed on **Windows Server**.

If your MetaDefender Storage Security is deployed on **Linux** based distributions, please follow [this article](/docs/mdss/integrations/how-to-add-a-smb-share-as-a-nfs-storage).

In order to integrate SMB Compatible Storage with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click on **Add -> Account** -> **SMB Compatible**

2. Give your [account](/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Enter the name of the user that will be used to access the SMB share
4. Enter the password of the above user.
5. Enter the IP address of the SMB server you wish to connect to.
6. Specify the port number used for the SMB connection, **445** being the default SMB port
7. Click on Next to finish the process.
8. From the left side menu, navigate to **Inventory**, click on **Add -> Unit ->** Choose the previously created account

9. Give your unit a unique name so you can identify it later.
10. Assign your unit to a Group
11. Indicate the specific share path on the SMB server from which you want to access files .
12. Click **Next** in order to finish the process.

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

Please note that SMB over QUIC is not supported at this time - only traditional SMB over TCP connections are compatible with this integration. See [[Windows] How to Expose an SMB Share as an NFS Storage Unit](/docs/mdss/integrations/windows-deployment--how-to-add-a-smb-share-as-a-nfs-storage-unit) for more details.
