<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli- -->

# A10 SSL Insight (SSLi)

Using A10’s [Thunder SSLi](https://www.a10networks.com/products/thunder-ssli-resources/) together with MetaDefender ICAP Server will help you scan your HTTP and decrypt SSL/TLS traffic flows for threats using all of the engines in MetaDefender Core. This guide describes the basic steps to get MetaDefender ICAP Server working with your A10 Thunder SSLi.

## [Sample Deployment Diagram](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#sample-deployment-diagram)

## [System Requirements](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#system-requirements)

The following systems are required to set up MetaDefender ICAP Server with an A10 Thunder SSLi

- A10 SSL Insight appliance (Thunder SSLi or Thunder CFW)
- MetaDefender ICAP Server
- MetaDefender Core

## [Configuring MetaDefender ICAP Server](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#configuring-metadefender-icap-server)

For installation and configuration quick guidelines see: 1. Quick Start with MetaDefender ICAP Server.

For detailed instructions see: 2. Installing or Upgrading MetaDefender ICAP Server and: [3. Configuring MetaDefender ICAP Server](/docs/mdicap/v5.14.1/configuration/metadefender-icap-server-configuration).

### [Note on MetaDefender ICAP Server Licensing](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#note-on-metadefender-icap-server-licensing)

MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [2.4. MetaDefender ICAP Server Licensing](/docs/mdicap/v5.14.1/installation/metadefender-icap-server-licensing).

## [Configuring A10 Thunder SSLi](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#configuring-a10-thunder-ssli)

The steps below describe the minimum configuration required for MetaDefender ICAP Server integration with A10 Thunder SSLi and was created based on ACOS 4.1.4_GR1-P2.

1. Open a web browser and launch the Thunder SSLi ACOS Web GUI. (Please refer to the A10 documentation for details on how to open the ACOS Web GUI. This guide was written with a presumption that you have already completed the device management configuration on the Thunder SSLi.)
2. Navigate to **System** > **App Template

3. Select **SSL Insight** to launch the SSLi App Centric Template (ACT)

4. Navigate to the first tab, **Wizard** on the **SSL Insight ACT** (if not automatically directed to it)**.**
5. Select **Custom** under the **Deployment** sub-tab, since the topology would require advanced configuration that needs an IP address to be assigned on the Thunder SSLi appliance. Click **NEXT** when done.

6. Under **Network**, Assign the device **IP Address** and **Default Gateway.** Click **NEXT** when done.

7. Import and assign the **SSL Cert. and Key.** Click **NEXT** when done.

8. Select traffic that needs to be bypassed from SSL inspection (for compliance), for e.g. Finance and Healthcare. Click **NEXT** when done.

9. Review your configuration and click **FINISH** when done.

10. Select **APPLY**.

11. The configuration will take a few seconds and a pop-up will indicate if the configuration was successful.
12. Navigate to the **Configuration** tab on the **SSL Insight ACT,** to set up OPSWAT security features.
13. Select **Edit Services** icon next to **Configured Services** on the right-hand side.

14. Under **Edit Services**, find and select **ICAP Based DLP / AV.

15. Check **Enable ICAP**, then clarify the MD ICAP Server IP Address.
16. The **ICAP Operation** contains a drop drown menu. The MD ICAP server can do REQMOD, RESPMOD, or both.

17. Make sure to add, OMSScanReq-A or OMSScanResp-A, respectively on the URL on the Request Service URI.

18. Select **Done** on the top right.
19. Finally, bind the ICAP policy to either the Decryption or Re-encryption Rule.

20. Select the Edit Rule

21. Under the **Configured Services** in the drop-down options, chose **ICAP Based DLP / AV.

22. Select **Deploy** on the to right.

23. Review and select **APPLY**.

24. Configurations will take a few seconds and a popup will indicate if the configuration was successful.

## [Testing the configuration](/docs/mdicap/v5.14.1/integrations/a10-ssl-insight--ssli-#testing-the-configuration)

To check that you configuration is working as expected try to download an Eicar test file over HTTPS [here](https://secure.eicar.org/eicar.com). If everything was set up properly you should see a blocking page similar to this:
