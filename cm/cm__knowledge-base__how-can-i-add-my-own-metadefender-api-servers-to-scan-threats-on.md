<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-add-my-own-metadefender-api-servers-to-scan-threats-on -->

# How can I add my own MetaDefender Core servers to scan threats on devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console, supported versions of the MetaDefender Core API, and all MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

If you or your organization have already deployed [OPSWAT MetaDefender Core](https://www.opswat.com/products/metadefender/core) servers, you now have the option to integrate (add) these servers to My OPSWAT Central Management to enable threat scanning of all your managed devices.

To do so, please follow the instructions below.

1. Log into your **My OPSWAT Central Management Console**, then navigate to **Settings>Global>MetaDefender Integration**.
2. Click the **Add Server** button, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/eiw448y3u8wihgygz8rt4t6aqtt3jfmszdlr36skhyz2wxpdmdf9in2q7b5qqksd.png)

3. In the pop-up, fill the required information into the fields provided, as illustrated below, including:
   - **Name**: the name of the server, for your own reference purposes.
   - **API Key:** the API key associated with your server. You can refer to [this guide on how to generate an API key](https://www.opswat.com/docs/mdcore/knowledge-base/how-to-generate-an-api-key-on-the-core-deployment-) if needed.
   - **Server Address:** your MetaDefender server’s URL.

![](https://uploads.developerhub.io/prod/97qW/6rlkro4nd131lk1huozisqbflijlw1fn6ldf4sec0hynaysjgjxrwv8o81d69vba.png)

4. Once all the fields are filled, click the **ADD** button to apply your changes, then click **Save**, to save all of the changes you’ve applied.

> **Pro Tip:**
>
> If you click the **TEST CONNECTION** button, My OPSWAT Central Management will try to connect to your server.
>
> If your server can be reached via the internet, the test will be successful. If your server cannot be reached online, the test will be unsuccessful.
>
> A failure can also occur if the API key is incorrect or invalid. Please ensure the API key is generated correctly and has the required permissions for integration.
>
> The most important thing, however, is that the managed devices from which you intend to scan files are able to connect to the server.

5. Finally, confirm with your **PIN**, as prompted.

> **Support:**
>
> For queries, concerns or issues regarding **Adding Your Own MetaDefender API Servers To** **My OPSWAT Central Management** **To Scan For Threats On Your Managed Devices**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
