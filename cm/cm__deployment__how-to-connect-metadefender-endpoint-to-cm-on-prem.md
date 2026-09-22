<!-- source: https://www.opswat.com/docs/cm/deployment/how-to-connect-metadefender-endpoint-to-cm-on-prem -->

# How to connect MetaDefender Endpoint to My OPSWAT Central Management On-premises

Administrators can connect the MetaDefender Endpoint to the My OPSWAT Central Management OnPrem servers.

MetaDefender Endpoint and  My OPSWAT Central Management OnPrem operate on a client-server model. Before establishing a connection between the client and the server in an on-premise or airgap environment, it is essential to ensure the client can connect to the server IP properly.

> **Tips**
>
> Open the web browser from the client side and access the IT Access Console. If you can access the Console, it's ready to install MetaDefender Endpoint. Otherwise, please check the network configuration.

![](https://uploads.developerhub.io/prod/97qW/ynn9uj0jt35lt3bttz0b8vwa5jmmi6fjwln41044ick65wm1032g8psv99b6snuq.png)

**Setup a secure connection on server**

After installing My OPSWAT Central Management OnPrem, administrators can access the Admin Console via the HTTP protocol (The default URL is http://<your server IP address>/). You also can see the URL during the setup wizard.

To enable HTTPS settings for MD IT Access OnPrem, please refer to the [How to Setup a Secure Connection](https://www.opswat.com/docs/cm/deployment/how-to-setup-a-secure-connection) guide. Once HTTPS is successfully configured, you can access the Console at ***https://<your-domain-onpremise>*** _ _log in.

> **Tips**
>
> Recommend to use a static IP for the server. It's the best if you setup a domain with **valid SSL certificate**. That is the most secure way to allow client connect  to server via HTTPS protocol. Follow [this guide](https://docs.opswat.com/macloud-sdp/metadefender-it-access-on-prem/secure-connection) to setup the secure connection.

Please refer to [Activating My OPSWAT Central Management On-Premises License](https://www.opswat.com/docs/cm/deployment/activating-my-opswat-central-management-on-premises-license) guide to activate your license so you can use MD IT Access Onpremise.

**Download MetaDefender Endpoint**

Click on the [+Device] button on the top-right to "Download MetaDefender Endpoint" for Distribution.

> **Warning**
>
> The file name includes basic information such as a hash of the server URL. Do not alter the filename. If you change the filename, MetaDefender Endpoint cannot connect to the IT Access Onprem properly

![](https://uploads.developerhub.io/prod/97qW/9hp3ny2nijrv17t9b0osoa1xqr46ewikxv4txua9hp7imsbfe33wbc3zj861hkp9.png)

On the "Download page", download the installer or portable client and install the agent on your devices:

![](https://uploads.developerhub.io/prod/97qW/un8uaz5kx87gi21a92zk8q5fbx7b1zkzwc8064b3wjavrs97wyx70uu1lp46nfn5.png)

Install MetaDefender Endpoint and make sure your device is connected to the server:

![](https://uploads.developerhub.io/prod/97qW/tsobobxoekuoj75nknitotfzvcgvc7hs39h4avu4xlmj4g1wnj60amb6h7g75awy.png)

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
