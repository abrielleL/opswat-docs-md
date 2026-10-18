<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-to-integrate-cerberus-sftp-with-mdss- -->

# How to Integrate Cerberus SFTP with MDSS?

> **Check Your Version:**
>
> This article applies to all supported MetaDefender Storage Security releases deployed on Windows and Linux systems

> **Info:**
>
> This guide provides instructions to setup Cerberus SFTP shared folder configuration to integrate with MDSS using the basic credentials (user/pass)

## What is Cerberus SFTP?

Cerberus SFTP Server enables organizations to become more efficient with fast, secure, compliant and easy file transfers. Homepage [Cerberus FTP Server - The Secure and Compliant FTP Server | Cerberus FTP Server](https://www.cerberusftp.com/)

## Step-by-Step Setup for Cerberus SFTP Server

> **Info:**
>
> Only supported on a Windows Server, recommended to install Cerberus on a Windows Server 2022

#### 1. **Download and Install Cerberus FTP Server**

- Go to the Cerberus FTP Server website and download the installer. [FTP Server Download | Cerberus FTP Server](https://www.cerberusftp.com/download/)
- Run the installer as an Administrator.
- Enter first account

#### 2. **Enable SSH for SFTP**

- SFTP requires SSH. Cerberus uses the built-in OpenSSH on Windows.
- Ensure OpenSSH is enabled on your system:
  - Go to **Settings > Apps > Optional Features**.
  - Install **OpenSSH Server** if it's not already installed.

#### 3. **Set Up an SFTP Listener**

![](https://uploads.developerhub.io/prod/k8zL/x7r5kyrimnfkkiyiuxgcunleym93oyx0m44syh3m59pq9us7h1l8kfsvpjq0nfx6.png)

How to setup an SFTP Listener (in case it doesn’t create by default):

- Open Cerberus FTP Server.
- Go to **Server Manager > Listeners**.
- Add a new listener:
  - **Protocol**: SFTP
  - **Port**: 22 (or another if needed)
  - **IP Address**: Choose the appropriate one (current server’s IP) or use `0.0.0.0` for all.

#### 4. **Configure Firewall and Router**

- Open port **22** (or your chosen port) on your firewall.

![](https://uploads.developerhub.io/prod/k8zL/powd3y38h6hethvh3lgtmikn8b05s7xef293xbulqnptp7abxze5r34as555dmcu.png)

![](https://uploads.developerhub.io/prod/k8zL/nutyzlgfrvfqzbtpo5gs0fw3qts7rue02jczvfyabetqfv8pirfbm7nu1hxwhr17.png)

- Set up **port forwarding** on your router to direct traffic to your server's internal IP (if needed)

#### 5. Mapping a folder with Cerberus local users

- Create a local user who has full permissions to the folder

![](https://uploads.developerhub.io/prod/k8zL/df3kk9iwf4h63y5z7xj453l0tp2w6635blp43d7g1j87tyyzgg1vo6fhun0hfd0d.png)

- Choose the user in the list
- Make sure the user is having the permission to login into SFTP protocol

![](https://uploads.developerhub.io/prod/k8zL/xkjv7zzd3jvnls8mtcha596bpcaofxexdgvzssxgl294qvid3v2elpq1mer84n7w.png)

- Make sure Simple directory mode option is disable

![](https://uploads.developerhub.io/prod/k8zL/9w1zrayxubx2emokl5vn7yyt2cdqsj0jfwv2thbvu8vugmau29ib9tuhkqme1f24.png)

- Click New Virtual Directory

![](https://uploads.developerhub.io/prod/k8zL/r8lgkcvh94imr6ct1hbfzvh12txqjhb87feghhtfy0ao2k17cbpibhlraknboop3.png)

- Open “Browse” to choose the mapping directory from your Windows server or shared folder

![](https://uploads.developerhub.io/prod/k8zL/jdra8w1nkkxhge5abz1009v0qvajw6t0b44yiihbo7s62on488tva6j7crg6uoag.png)

![](https://uploads.developerhub.io/prod/k8zL/ozn7gqhpth5yzz96nm1r4ldobea3jzx2sl30otpow34xthss1z15qvypyk34rc1z.png)

- Enter the shared name and give all permissions to the folder (save the shared name to configure later on from MDSS)

![](https://uploads.developerhub.io/prod/k8zL/iqjp1ki6e7tzj044ljb8hzcpaj2q2sddmodxaykldbd33i96emff6k4otn6kssv0.png)

- Now the shared path is good to go integrating with MDSS, we could try with WinSCP first to see if it works, share path should come with the format as //CerberusIP/Name as configured, username and password are the credentials configured to the folder.

![](https://uploads.developerhub.io/prod/k8zL/m5ao35v9rpt2mhdye6z1n9nod2xle784bforsmolno10r2b9nvkisy0x0wmt2iih.png)

## Mapping a shared folder with AD users via Cerberus group

As Cerberus is allowing AD integration, we could also integrate an AD or LDAP for users management

1. To add an AD, simply go to Authentication> AD users > Add New Domain

![](https://uploads.developerhub.io/prod/k8zL/3m2jyw94aelefu6ab296qgsfzpiv6c7crry5t88fzsr6nzju2ucni1oasm3a9vld.png)

Fill in domain name

![](https://uploads.developerhub.io/prod/k8zL/w3mtque6d20ohaq4jrncwai1qteititp1qjro6n9jg319ixn59xjcppsa3mhyel8.png)

We could modify the domain later on after added

![](https://uploads.developerhub.io/prod/k8zL/4habu3kuc8ktdrk11bpdibedcvyc9rzertqkwby3u18nhmmxdbviknlj7nrotbat.png)

After connected successfully to the AD, the users list could be displayed at Users tab

![](https://uploads.developerhub.io/prod/k8zL/ot816o7beqvbu2fusffiyea456lrdzgab0e46ovutl5xfr4df7dvlt5p8btlrozs.png)

Synchronized AD users could be unable to map a Virtual Directory, to map a folder to multiple (AD) users,  we could use a Cerberus group

2. Add a group from User manager

![](https://uploads.developerhub.io/prod/k8zL/doi9bx6gy10rvrl9ird8ylfuvffkyz90f4mjxaw9skqj9p7ccyhcqo0kiavtm6vz.png)

3. Make sure Single mode is disabled at Virtual Directories tab for the group

![](https://uploads.developerhub.io/prod/k8zL/a92npvfyybgjksxtgfj84chix420pl1jaax7jl4yykbfiz5vhquhasfhld14enne.png)

4. Create a New mapping, map a directory into the group

![](https://uploads.developerhub.io/prod/k8zL/01ogi19kmc1wof2g67atpxwfqb8t81zprk2ifq7g2lbza3ecefzazasgzaw5emy8.png)

5. Assign the users into the created Cerberus group

a. Local users: go to User profile, and assign a primary group

![](https://uploads.developerhub.io/prod/k8zL/i95bsr1f9hvdssp97vmd4lmn5nw7p8nrzi4tdz74r0p0yrk1wa0am6oz9byq05jv.png)

b. AD users

![](https://uploads.developerhub.io/prod/k8zL/m5fz97uf81lrvx2lv15cao4vfuccsg9ck4vn0scbz9oqsicsbpbb36rairgmuqw8.png)

![](https://uploads.developerhub.io/prod/k8zL/qgzqwpn417mbbpw5odc2oa4zlljwf8iie7h3lmz8rf3ur9f67lkwnxsnoagv1wwb.png)

Head to the user’s Directory, the group mapped folder should be displayed

![](https://uploads.developerhub.io/prod/k8zL/w8sytpjv5bk34g7898ph0yb7nwufit5tqq4x740esyaj77jvns87so7wxympiv6t.png)

From then on, we could configure in MDSS the SFTP mapping Directory for the assigned users to the group with the share path format as //CerberusIP/Name

> **Info:**
>
> Format should be **username@domainame** for username

server: <Ipaddress>

Share Path //<ipaddress>/Groupshared

![](https://uploads.developerhub.io/prod/k8zL/pz93e4nf5hy6ufsljzr0j79jxh506pq0rw9a19oifwndej8bqb4or3h75v5lpj9l.png)

![](https://uploads.developerhub.io/prod/k8zL/gqvjn2wju8mdxedaaz7cmgcza83d4i850hnc7z7q7wmfxk8fqszv3xx4rjcg4a54.png)

## Webhooks

We’ve prepared MDSS to be able to accept an API request sent by Cerberus

With the request, we need some information as well:

1. A header with an API key for auth
2. A payload containing a storageclient id and a metadata

### Example:

`{`

`"metadata": "{'Name': 'folder1/folder2/test-file.exe' }",`

`"storageClientId": '0c5454e3-d576-44c5-8ce4-cdc078011d0b'`

`}`

> **Warning:**
>
> Scans with Deep CDR enabled have limited functionality, this is will be resolved in future releases.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
