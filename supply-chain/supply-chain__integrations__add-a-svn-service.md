<!-- source: https://www.opswat.com/docs/supply-chain/integrations/add-a-svn-service -->

# Add A SVN Service

In order to integrate **SVN** with MetaDefender Software Supply Chain, please follow these steps:

1. From the left side menu, navigate to **Inventory** and choose **SVN**.
2. Give your connection a name so you can easily identify it later.

![](https://uploads.developerhub.io/prod/jdK6/kphi6k1nz8n318zge5fl0fxy1n2ftmsqj4kjbej1buammcs4wv1r64yfyakdb9bn.png)

3. Enter your SVN domain.
4. Enter your **SVN User Name** and **Password**
5. Select **Add Connection**  in order to finish the process.

> **Info**
>
> Our application currently supports **only WebDAV-SVN interface integration**. This means that when registering an SVN connection, the SVN server **must be configured with Apache and the WebDAV-SVN module enabled**, allowing access via **HTTP GET and POST requests**.
>
> If the required WebDAV-SVN setup is not present on the server, the integration will fail.
