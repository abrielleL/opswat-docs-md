<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/configuration/configuring-with-metadefender-core -->

# Configuring with MetaDefender Core

MetaDefender Kiosk requires MetaDefender Core for multi-scanning functionality.

Setting up MetaDefender Core with MetaDefender Kiosk consists of the following steps:

### [Detecting the MetaDefender Core server URL](/docs/mdkiosk/v4.8.5/configuration/configuring-with-metadefender-core#detecting-the-metadefender-core-server-url)

If MetaDefender Core is installed on a remote machine from Kiosk, the server URL must be specified.

1. Access your MetaDefender Kiosk Management Console at `http(s)://<ip or dns>:8009`. You can also access the Kiosk Management Console using Windows **Start** > **OPSWAT** > **MetaDefender Kiosk Management Console**.
2. Click **Configuration** and enter your MetaDefender Core URL

3. Additional backup servers can be added in case the primary server becomes inaccessible, its license expires, or other issues the primary server might encounter.

### [Authenticating the Core connection](/docs/mdkiosk/v4.8.5/configuration/configuring-with-metadefender-core#authenticating-the-core-connection)

You must authenticate your connection by obtaining an API key from the MetaDefender Core Management Console.

Info

MetaDefender Kiosk requires the MetaDefender Core API key to be assigned an `Administrator` role

1. Access the MetaDefender Core Management Console
2. Select `User Management`

3. Click the desired user with an Administrator role and copy the contents of the `API key` field. If an API key has not been previously generated click the `Generate` link and make sure to save changes.

4. Return to the MetaDefender Kiosk Management Console and click the `Configuration` tab
5. Paste your Core API key value in the `API Key` field

### [Associating workflows in Kiosk to workflows in Core](/docs/mdkiosk/v4.8.5/configuration/configuring-with-metadefender-core#associating-workflows-in-kiosk-to-workflows-in-core)

Refer to [Selecting a Server to Process Files](/docs/mdkiosk/v4.8.5/operating/selecting-a-server-to-process-files)
