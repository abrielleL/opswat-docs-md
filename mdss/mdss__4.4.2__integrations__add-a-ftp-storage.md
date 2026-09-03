<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/add-a-ftp-storage -->

# Add an FTP Storage

We recommend increasing the maximum number of concurrent connections allowed by your FTP server from its default setting. This helps improve performance and prevent connection bottlenecks during high-load operations. After that, make sure to set the **FTP_MAX_CONNECTIONS** environment variable in MDSS

In order to integrate FTP with MetaDefender Storage Security please follow these steps:

1. From the left side menu, navigate to **Storage units**, click on **Add storage unit** and choose **FTP**

2. Give your [account](/docs/mdss/4.4.2/operations/accounts-and-groups) a name so you can easily identify it later
3. Give your storage a name so you can easily identify it later
4. **Host:** Enter the IP address of the FTP server you wish to connect to.
5. **Port**: Specify the port number used for the FTP connection, typically **21** for standard FTP
6. Input the **Username** required to authenticate your access to the FTP server. (The user should have at least read and write security permissions)
7. Provide the **Password** associated with the username**.**
8. Indicate the specific directory path on the FTP server from which you want to access files .

Info

The folder path should start from the root of the shared directory, not the absolute path of the server. For example, if the shared directory is `/shared_files` and you want to access a folder named `documents` within it, you would enter `documents` as the folder path, rather than the full path like `/home/user/shared_files/documents`

6. Click **Continue** in order to finish the process.

Info

If you use a hostname in the host portion of IPv4/v6 socket address, the program may show a non-deterministic behavior. The socket address will be resolved differently into an actual IPv4/v6 address, depending on the results from DNS resolution and/or the host configuration. For deterministic behavior use a numeric address in host portion.
