<!-- source: https://www.opswat.com/docs/macloud-sdp/metadefender-it-access-on-prem/how-to-connect-metadefender-endpoint-to-metadefender-it-access-o -->

# How to connect MetaDefender Endpoint to MetaDefender IT Access OnPrem

Administrators can connect the MetaDefender Endpoint to the MetaDefender IT Access OnPrem servers. MetaDefender Endpoint and MetaDefender IT Access OnPrem operate on a client-server model. Before establishing a connection between the client and the server in an on-premise or airgap environment, it is essential to ensure the client can connect to the server IP properly.

Tips

Open the web browser from the client side and access the IT Access Console. If you can access the Console, it's ready to install MetaDefender Endpoint. Otherwise, please check the network configuration.

**Setup a secure connection on server**

After installing MetaDefender IT Access OnPrem, administrators can access the Admin Console via the HTTP protocol (The default URL is http://<your server IP address>/). You also can see the URL during the setup wizard.

To enable HTTPS settings for MD IT Access OnPrem, please refer to the "[How to setup a secure connection](https://docs.opswat.com/macloud-sdp/metadefender-it-access-on-prem/secure-connection)" guide. Once HTTPS is successfully configured, you can access the Console at ***https://<your-domain-onpremise>*** _ _log in.

Tips

Recommend to use a static IP for the server. It's the best if you setup a domain with **valid SSL certificate**. That is the most secure way to allow client connect to server via HTTPS protocol. Follow [this guide](https://docs.opswat.com/macloud-sdp/metadefender-it-access-on-prem/secure-connection) to setup the secure connection.

Please refer to this '[Activating MetaDefender IT Access Onpremise License](https://docs.opswat.com/macloud-sdp/metadefender-it-access-on-prem/activating-metadefender-it-access-onpremse-license)' guide to activate your license so you can use MD IT Access Onpremise.

**Download MetaDefender Endpoint**

Click on the [+Device] button on the top-right to "Download MetaDefender Endpoint" for Distribution.

Warning

The file name includes basic information such as a hash of the server URL. Do not alter the filename. If you change the filename, MetaDefender Endpoint cannot connect to the IT Access Onprem properly

On the "Download page", download the installer or portable client and install the agent on your devices:

Install MetaDefender Endpoint and make sure your device is connected to the server:
