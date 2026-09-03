<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/huawei-oceanstor -->

# Huawei OceanStor

**External documentation**

You can find detailed instruction on Huawei storage setup with a 3rd party file protection system at the this URL:

*- Huawei OceanStor V5 Storage*: <https://support.huawei.com/enterprise/en/doc/EDOC1100138521/69ba9dda/file-antivirus>

*- Huawei OceanStor Dorado All-Flash Storage*: <https://support.huawei.com/enterprise/en/doc/EDOC1100214966?idPath=7919749%7C251366268%7C250389224%7C21462743%7C24030109>

*- Huawei OceanStor Hybrid Flash Storage*: <https://support.huawei.com/enterprise/en/doc/EDOC1100247956?idPath=7919749%7C251366268%7C250389224%7C251366266%7C254051431>

- *For the MetaDefender ICAP Server integration:* you should follow the *Configuring Antivirus Servers* section in the setup instruction on the Huawei site: <https://support.huawei.com/enterprise/en/doc/EDOC1100138521/9f834e59/configuring-antivirus-servers>.

*-* *Huawei OceanStor Pacific Scale-Out Storage*: <https://support.huawei.com/enterprise/en/doc/EDOC1100310889?idPath=7919749%7C251364444%7C21430817%7C251366260%7C251711085>

## [Supported features](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#supported-features)

The following OPSWAT technologies are supported by MetaDefender ICAP Server when integrated to Huawei OceanStor via FILEMOD:

- [Multiscanning](https://www.opswat.com/technologies/multiscanning)
- [Deep Content Disarm & Reconstruction](https://www.opswat.com/technologies/data-sanitization)
- [Proactive Data Loss Prevention](https://www.opswat.com/technologies/proactive-data-loss-prevention)

## [Configuration](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#configuration)

Things to consider during setup (in this specific order):

### [Huawei Antivirus Agent](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#huawei-antivirus-agent)

Deploy the Huawei Antivirus Agent on same host with the MetaDefender ICAP Server

For Huawei OceanStor V5

After you deploy the Huawei Antivirus Agent, edit the agentConfig.ini file (default location C:\Program Files (x86)\Huawei\Antivirus Agent\cfg) by adding the name of the MetaDefender ICAP Server service executable image mdicapsrv.exe in the Symantec Protection Engine section as highlighted below:

Restart the antivirus agent program. On the *Services* page, right-click *Antivirus Agent Watchdog* and choose *Restart* to restart the antivirus agent program. The antivirus agent configuration is completed.

### [Permissions](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#permissions)

#### [Create a privileged user for antivirus on the storage](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#create-a-privileged-user-for-antivirus-on-the-storage)

For Huawei OceanStor V5

For Huawei OceanStor Dorado All-Flash Storage & Huawei OceanStor Hybrid Flash Storage

For Huawei OceanStor Pacific Scale-Out Storage

#### [MetaDefender ICAP Server service](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#metadefender-icap-server-service)

1. Update the MetaDefender ICAP Server service account to use the same privileged user configured for the Huawei Antivirus Agent. This account must have Administrator rights

2. Restart the MetaDefender ICAP Server service. On the Services page, right-click OPSWAT MetaDefender ICAP Server and choose Restart to restart
3. Restart the Antivirus Agent Watchdog. On the Services page, right-click Antivirus Agent Watchdog and choose Restart to restart the antivirus agent program. The antivirus agent configuration is complete.

#### [Configuring the Shared Key](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#configuring-the-shared-key)

Huawei OceanStor Pacific Scale-Out Storage

You are advised to configure a shared key for the antivirus agent and storage system. If no shared key is configured, the storage system fails to connect to the antivirus agent.

Refer to the Security Configuration Guide in the **External documentation** section to configure the shared key

### [Huawei OceanStor](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#huawei-oceanstor)

For Huawei OceanStor V5

When setting up with MetaDefender ICAP Server you should be using the *Symantec Protection Engine* profile as per below screenshot

You can now test it by clicking on the “Test” button:

For Huawei OceanStor Dorado All-Flash Storage & Huawei OceanStor Hybrid Flash Storage

Select OPSWAT MetaDefender ICAP Server as below

Huawei OceanStor Pacific Scale-Out Storage

Select OPSWAT MetaDefender ICAP Server as below

### [Storage share](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#storage-share)

Info

Make sure the same account that is used for Huawei Antivirus Agent and the MetaDefender ICAP Server has permission on the CIFS share as per below screenshot:

## [Testing](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#testing)

Test the integration by uploading the [EICAR Standard Anti-Virus Test File](https://www.eicar.org/?page_id=3950) to the storage share to see the file getting deleted by the MetaDefender ICAP Server.

### [MD ICAP Server Configuration](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#md-icap-server-configuration)

Refer to [Filemod Configuration](/docs/mdicap/v5.14.1/configuration/filemod-configuration)

## [Examples](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#examples)

### [Content disarm and reconstruction](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#content-disarm-and-reconstruction)

Original file upload:

MetaDefender ICAP Server will replace it with the sanitized version automatically:

- To display " User Name" on ICAP History for FileMod, please go to **ICAP History** and enable the checkbox for "User Name" as below

- ICAP History will be display like this, Client IP and User Name will be displayed

### [Data loss prevention & Multiscanning](/docs/mdicap/v5.14.1/integrations/huawei-oceanstor#data-loss-prevention--multiscanning)

Depend on configuration of MD ICAP Server, when Proactive DLP is enabled and a file with sensitive information is uploaded or uploading an infected file then the file will get deleted automatically or will be moved to quarantine path
