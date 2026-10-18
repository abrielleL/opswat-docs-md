<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/add-a-sftp-storage -->

# Add an SFTP Storage

| Product Specification Requirements | Version |
| ---- | ---- |
| Secure File Transfer Protocol (SFTP) | OpenSSH__for Windows_8.1p1 OpenSSH_7.9p1 Debian-10+deb10u2 OpenSSL 1.1.1(for Linux) |

> **IMPORTANT**
>
> Integration with SFTP storage is achieved through the SSH File Transfer Protocol (SFTP). Before proceeding, please ensure that this protocol is enabled on your system. Our application is compatible with SFTP servers that adhere to the standard SSH File Transfer Protocol, including Cerberus SFTP for Windows and the OpenSSH SFTP subsystem, which is typically included with Linux and Unix SSH servers.

> **Info**
>
> We recommend increasing the maximum number of concurrent connections allowed by your SFTP server from its default setting. This helps improve performance and prevent connection bottlenecks during high-load operations. After that, make sure to set the **SFTP_CONNECTION_POOL_MAX** environment variable in MDSS, which is at 100 by default.

In order to integrate SFTP with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Inventory**, click **Add New** > **Account**, choose **SFTP (SSH File Transfer Protocol)** and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/rzzvbqit5l63da4ow2lqu5y533bdsj9i8hct5c59vxazmt1jasnjh7hix194g4e1.png)

2. Give your [account](https://www.opswat.com/docs/mdss/operations/accounts-and-groups) a name so you can easily identify it later
3. Input the **Username** required to authenticate your access to the SFTP server. (The user should have at least read and write security permissions)
4. Provide the **Password** associated with the username provided at step 3.
5. **Host:** Enter the IP address of the SFTP server you wish to connect to.
6. **Port**: Specify the port number used for the SFTP connection, typically **22** for standard SFTP
7. Click **Next** in order to finish the process of adding the account
8. From the left side menu, navigate to **Inventory**, click **Add New** > **Unit**, choose the previously created account and click **Next**

![](https://uploads.developerhub.io/prod/k8zL/63a2pzeldalr62e97huuc6u3ed9b3ea2h9acln0gp4cayghv8hntbm8vmk31og6c.png)

9. Give your unit an unique name so you can easily identify it later.
10. Assign your unit to a Group
11. (Optional) Indicate the specific directory path on the SFTP server from which you want to access files.

> **Info**
>
> The folder path should start from the root of the shared directory, not the absolute path of the server. For example, if the shared directory is `/shared_files` and you want to access a folder named `documents` within it, you would enter `documents` as the folder path, rather than the full path like `/home/user/shared_files/documents`

9. Click **Next** in order to finish the process.

> **Info**
>
> A SSH connection is required to be enabled in order to connect to a Unix-based system **SharePath.** If the SSH is not installed please run the following commands:
>
> `sudo apt-get update`
>
> `sudo apt-get upgrade`
>
> `sudo apt-get install openssh-client`

> **Info**
>
> If you use a hostname in the host portion of IPv4/v6 socket address, the program may show a non-deterministic behavior. The socket address will be resolved differently into an actual IPv4/v6 address, depending on the results from DNS resolution and/or the host configuration. For deterministic behavior use a numeric address in host portion.

> **Warning**
>
> Please make sure that **Enable transfer resume/transfer to temporary filename** option is set on **Disable** if **using 3rd party** **SFTP clients** (if it allows this feature).
>
> See the image below for  **WinSCP client**.

![](https://uploads.developerhub.io/prod/k8zL/j1vt1rpdl2bc5gi1rsez0j1myr1il0r9yw2yie1djkeyozrmznuj5y9bgs0slpe0.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
