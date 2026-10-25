<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator -->

# F5 SSL Orchestrator

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Sample Deployment Diagram

Using F5's SSL Orchestrator together with MetaDefender ICAP Server will help you scanning your non-SSL and decrypted SSL traffic flow for threats using all of the engines in MetaDefender Core. This guide describes the basic steps to getting MetaDefender ICAP Server working with your F5 SSL Orchestrator.

## [System Requirements](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#system-requirements)

The following systems are required to set up MetaDefender ICAP Server with an F5 SSL Orchestrator

- F5 SSL Orchestrator
- MetaDefender ICAP Server
- MetaDefender Core

## [Configuring MetaDefender ICAP Server](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#configuring-metadefender-icap-server)

For installation and configuration quick guidelines see: 1. Quick Start with MetaDefender ICAP Server.

For detailed instructions see 2. Installing or Upgrading MetaDefender ICAP Server and [3. Configuring MetaDefender ICAP Server](/docs/mdicap/v5.15.0/configuration/metadefender-icap-server-configuration).

### [Note on MetaDefender ICAP Server Licensing](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#note-on-metadefender-icap-server-licensing)

MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [2.4. MetaDefender ICAP Server Licensing](/docs/mdicap/v5.15.0/installation/metadefender-icap-server-licensing).

## [Configuring F5 SSL Orchestrator](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#configuring-f5-ssl-orchestrator)

The following configuration steps should be done from the F5 SSL Orchestrator Management Console interface. The steps below describe the minimum configuration required for MetaDefender ICAP Server integration with F5 SSL Orchestrator and was created based on SSL Orchestrator v3.0.

Open a web browser and load the SSL Orchestrator Management Console. (Please refer to the SSL Orchestrator manual for details about how to open the BIG IP Management Console.)

This guide was written with a presumption that you have already completed the [General Properties](https://support.f5.com/kb/en-us/products/ssl-orchestrator/manuals/product/f5-herculon-ssl-orchestrator-setup-13-0-0/4.html#guid-3bca9642-cfaf-4f9c-840e-9601f50b7b90) configuration in the SSL Orchestrator.

### [Configuring the ICAP service](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#configuring-the-icap-service)

1. Navigate to **SSL Orchestrator** > **Configuration
2. Select **ICAP / SWG Services** under the **Services** tab

3. Click **Add** to add a new ICAP service

4. In the **Name** field, type a name for your configuration
5. Select **ICAP** as the **Service type**
6. Add your MetaDefender ICAP Server's IP and port to the **ICAP Devices**
7. Select the **Headers** mode. "Default" can be used.
8. Select **TCP Connections**. *OneConnect* can be used if you enabled persistent connections in your MetaDefender ICAP Server (enabled by default) otherwise use *Separate*.
9. Select "Load Balanced" as the **Type**. You can find more information about it [here](https://support.f5.com/kb/en-us/products/ssl-orchestrator/manuals/product/f5-herculon-ssl-orchestrator-setup-13-1-0-iapp-3-0/5.html#guid-3aaa1035-268d-4710-be4e-5bb5310b300b).
10. You can use "reqmod" and "respmod" as the values for **Request** and **Response** fields
11. Select your **ICAP Policy** if you have any
12. Set 0 as the **Preview Max. Length**
13. Select your preferred **Server Failure Handling** (Next Service Chain or Reset Connection)
14. Select if you would like to send only HTTP/1.1 or both HTTP/1.0 and HTTP/1.1 requests to the ICAP service in **Send HTTP/1.0 Requests to ICAP**
15. Set your **Addition iRule** if you have any
16. Click **Finished**
17. Click **Save**

## [Testing the configuration](/docs/mdicap/v5.15.0/integrations/f5-ssl-orchestrator#testing-the-configuration)

To check that you configuration is working as expected try to download an eicar testfile over HTTPS [here](https://secure.eicar.org/eicar.com). If everything was setup properly you should see a blocking page similar to this:
