<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss- -->

# How to Integrate Cerberus SFTP with MDSS?

This article applies to all supported MetaDefender Storage Security releases deployed on Windows and Linux systems

Info:

This guide provides instructions to setup Cerberus SFTP shared folder configuration to integrate with MDSS using the basic credentials (user/pass)

## [What is Cerberus SFTP?](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#what-is-cerberus-sftp)

Cerberus SFTP Server enables organizations to become more efficient with fast, secure, compliant and easy file transfers. Homepage [Cerberus FTP Server - The Secure and Compliant FTP Server | Cerberus FTP Server](https://www.cerberusftp.com/)

## [Step-by-Step Setup for Cerberus SFTP Server](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#step-by-step-setup-for-cerberus-sftp-server)

Info:

Only supported on a Windows Server, recommended to install Cerberus on a Windows Server 2022

#### [1. **Download and Install Cerberus FTP Server**](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#1-download-and-install-cerberus-ftp-server)

- Go to the Cerberus FTP Server website and download the installer. [FTP Server Download | Cerberus FTP Server](https://www.cerberusftp.com/download/)
- Run the installer as an Administrator.
- Enter first account

#### [2. **Enable SSH for SFTP**](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#2-enable-ssh-for-sftp)

- SFTP requires SSH. Cerberus uses the built-in OpenSSH on Windows.
- Ensure OpenSSH is enabled on your system:

  - Go to **Settings > Apps > Optional Features**.
  - Install **OpenSSH Server** if it's not already installed.

#### [3. **Set Up an SFTP Listener**](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#3-set-up-an-sftp-listener)

How to setup an SFTP Listener (in case it doesn’t create by default):

- Open Cerberus FTP Server.
- Go to **Server Manager > Listeners**.
- Add a new listener:

  - **Protocol**: SFTP
  - **Port**: 22 (or another if needed)
  - **IP Address**: Choose the appropriate one (current server’s IP) or use `0.0.0.0` for all.

#### [4. **Configure Firewall and Router**](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#4-configure-firewall-and-router)

- Open port **22** (or your chosen port) on your firewall.

- Set up **port forwarding** on your router to direct traffic to your server's internal IP (if needed)

#### [5. Mapping a folder with Cerberus local users](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#5-mapping-a-folder-with-cerberus-local-users)

- Create a local user who has full permissions to the folder

- Choose the user in the list
- Make sure the user is having the permission to login into SFTP protocol

- Make sure Simple directory mode option is disable

- Click New Virtual Directory

- Open “Browse” to choose the mapping directory from your Windows server or shared folder

- Enter the shared name and give all permissions to the folder (save the shared name to configure later on from MDSS)

- Now the shared path is good to go integrating with MDSS, we could try with WinSCP first to see if it works, share path should come with the format as //CerberusIP/Name as configured, username and password are the credentials configured to the folder.

## [Mapping a shared folder with AD users via Cerberus group](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#mapping-a-shared-folder-with-ad-users-via-cerberus-group)

As Cerberus is allowing AD integration, we could also integrate an AD or LDAP for users management

1. To add an AD, simply go to Authentication> AD users > Add New Domain

Fill in domain name

We could modify the domain later on after added

After connected successfully to the AD, the users list could be displayed at Users tab

Synchronized AD users could be unable to map a Virtual Directory, to map a folder to multiple (AD) users, we could use a Cerberus group

2. Add a group from User manager

3. Make sure Single mode is disabled at Virtual Directories tab for the group

4. Create a New mapping, map a directory into the group

5. Assign the users into the created Cerberus group

a. Local users: go to User profile, and assign a primary group

b. AD users

Head to the user’s Directory, the group mapped folder should be displayed

From then on, we could configure in MDSS the SFTP mapping Directory for the assigned users to the group with the share path format as //CerberusIP/Name

Info:

Format should be **username@domainame** for username

server: <Ipaddress>

Share Path //<ipaddress>/Groupshared

## [Webhooks](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#webhooks)

We’ve prepared MDSS to be able to accept an API request sent by Cerberus

With the request, we need some information as well:

1. A header with an API key for auth
2. A payload containing a storageclient id and a metadata

### [Example:](/docs/mdss/4.4.2/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss-#example)

`{`

`"metadata": "{'Name': 'folder1/folder2/test-file.exe' }",`

`"storageClientId": '0c5454e3-d576-44c5-8ce4-cdc078011d0b'`

`}`

Warning:

Scans with Deep CDR enabled have limited functionality, this is will be resolved in future releases.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
