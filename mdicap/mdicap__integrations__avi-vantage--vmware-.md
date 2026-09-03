<!-- source: https://www.opswat.com/docs/mdicap/integrations/avi-vantage--vmware- -->

# Avi Vantage (VMware)

This documentation is based on Avi Vantage version 20.1.6 and is the minimum configuration required to integrate Avi Vantage and MetaDefender ICAP Server.

---

## [Prerequisities](/docs/mdicap/integrations/avi-vantage--vmware-#prerequisities)

- Avi Vantage is installed and licensed
- MetaDefender ICAP Server is installed and license is activated

  - For installation and configuration quick guidelines see: auto$. For detailed instructions see:auto$ and: [MetaDefender ICAP Server configuration](/docs/mdicap/configuration/metadefender-icap-server-configuration).
  - MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [MetaDefender ICAP Server Licensing](/docs/mdicap/installation/metadefender-icap-server-licensing).
- MetaDefender Core is installed and license is activated
- Web browser access to the Avi Vantage web GUI. (Please refer to the VMware documentation for details on how to access the Avi Vantage web GUI. This guide was written with a presumption that you have already completed the device management configuration on the Avi Vantage device and it is currently functioning as a proxy.)

## [Integration Steps](/docs/mdicap/integrations/avi-vantage--vmware-#integration-steps)

### [Configuring an ICAP Pool and Pool Group](/docs/mdicap/integrations/avi-vantage--vmware-#configuring-an-icap-pool-and-pool-group)

Navigate to **Application** > **Pool Group** to create a pool group. Provide a name for the group. You will create the necessary Pool Group Members in the next step. The field for the *Fail Action* under the **Pool Group Failure Settings** needs to have no selection (empty).

Click **+Add Pool Group Member** on the Pool Group page. This is where you will specify the ICAP server port (default = 1344) and the OPSWAT ICAP Server IP.

In the Servers tab, enter the information for the OPSWAT ICAP Server. All other settings are default. When done, click **Save**.

### [Configuring an ICAP Profile](/docs/mdicap/integrations/avi-vantage--vmware-#configuring-an-icap-profile)

Navigate to **Templates > Profiles > ICAP Profile** to create an ICAP Profile. In this section you will need to provide a name for the profile and assign it the Pool Group you created earlier.

**Service URL:** /OMSScanReq-AV

On the bottom section, make note of the **Action** setting. The values for these settings are dependent upon your organization's security policies. When finished, click **Save**.

### [Assign ICAP Profile to the Virtual Service](/docs/mdicap/integrations/avi-vantage--vmware-#assign-icap-profile-to-the-virtual-service)

Navigate to **Application** > **Virtual Service**, select the desired virtual service, click **Edit.** In the ICAP Profile, select the ICAP profile you created in the previous step. Click **Save**.

### [Create an HTTP Security Policy](/docs/mdicap/integrations/avi-vantage--vmware-#create-an-http-security-policy)

Create a security policy to define the rules which determine when ICAP scanning should be performed. Navigate to **Application** > **Virtual Service**, select the desired virtual service, and click on **Edit**. Select **Policies** > **HTTP Security**, and create a new rule with the following options:

- Rule Name: the rule name specified here will appear in the Avi Vantage logs. We recommend that you use a descriptive name to to allow easier troubleshooting.
- Select match criteria for the ICAP requests: **HTTP Method***is not in***(GET).** This instructs Avi Vantage to forward all requests to the ICAP Server for scanning, except for GET requests.
- Select **Enable ICAP** as the action
- When finished, click **Save**.

Notes regarding ICAP support in Avi Vantage

- ICAP is not supported for HTTP/2 virtual services.
- The Avi Vantage ICAP Client only works in request mode (REQMOD). The Avi Vantage ICAP client does not work in the response (RESPMOD) context.
