<!-- source: https://www.opswat.com/docs/mdendpoint/installation/install-from-myopswatcentralmanagement -->

# Installing & Updating MetaDefender Endpoint in My OPSWAT Central Management

## Download MetaDefender Endpoint package

1. Log into your **My OPSWAT** portal.
2. Go to **Home** -> **MetaDefender Endpoint** and click the **Download** button, as illustrated in the screenshot below.
3. Click the **MetaDefender Endpoint** tab, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/2x2P/u7la1wegah6lx4fh1y9wsbq8j6i2bfws5b23o7imkvziwtmloimlvi7oknpd8x4q.png)

![](https://uploads.developerhub.io/prod/2x2P/vgtt4j52hyxh6mscc9kdz5sa22l4jg0dzfmjjbrjz8vcey24b61ewo4c6khui3x2.png)

4. Choose the platform which you want to install the MetaDefender Endpoint
   - You need to download **two files (.zip and .yml)** before uploading to the server.
   - Persistent:
     - Persistent Agent [<platform>]
     - Persistent Agent Descriptor [<platform>]
   - On-Demand:
     - On-Demand Agent [<platform>]
     - On-Demand Agent Descriptor [<platform>]

## Upload the MetaDefender Endpoint package to the My OPSWAT Central Management On-premises

**Step 1:** Login to My OPSWAT Central Management

![](https://uploads.developerhub.io/prod/2x2P/w1lu519bo33bwgk2dttiez0uo8dt78zcgrv9vrjx2e1ye05ycbe7r5152e6cw95m.png)

**Step 2:** Navigate to *Settings > Update Packages > Upload*

**Step 3:** Upload the file to the corresponding Component Name, depending on the platform installers you downloaded.

> **NOTE**
>
> Please make sure to **keep the file names** exactly as they are when downloaded. For example:
>
> - windows_installer.zip
> - windows_installer.yml
>
> Changing the file names will result in a failed upload.

![](https://uploads.developerhub.io/prod/2x2P/5kfrjizh9c0d1668o2uf9mkrnnvgxc639cmmi5h4t1i2c7qf40x8kta8ggamz354.png)

![](https://uploads.developerhub.io/prod/2x2P/b1dq7ri8yr7sle289usmak1dt05oc0q4466owa28bsw3yt1byre79l7w7d188hm8.png)

**Step 4:** When uploading, the admin must **upload two files**: zip and YML file.

> **NOTE**
>
> Please make sure to upload only newer versions of the installers compared to the current ones. Uploading the same or older versions will result in a failed upload.

![](https://uploads.developerhub.io/prod/2x2P/o1n1vpjo739ees60g20vb9qhf4ds66zidr6fcqomf7ruxv0ge4136oimdtwe9o7t.png)

![](https://uploads.developerhub.io/prod/2x2P/3hyau4llsq76dkmtspin9ndt8hxia8evemjog4jg5zaxzyk826yeu28qwezyc7r3.png)

For more information on product updates, please refer to this link: [Product Updates - My OPSWAT Central Management](https://www.opswat.com/docs/cm/configurations/product-updates#metadefender-endpoint)
