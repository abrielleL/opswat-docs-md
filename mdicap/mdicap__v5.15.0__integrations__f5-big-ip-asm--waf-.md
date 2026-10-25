<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf- -->

# F5 BIG IP ASM (WAF)

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Using F5's Web Application Firewall solution together with MetaDefender ICAP Server will help you prevent malware reaching your web application by analyzing files being uploaded with multiple AV engines in MetaDefender Core. You can also add MetaDefender ICAP Server technology to your existing virtual server by using MetaDefender's [iApp template](/docs/mdicap/v5.15.0/integrations/icap-server-iapp-template). This is a step by step guideline on how to enable threat prevention functionality for F5 BIG IP ASM by leveraging MetaDefender ICAP Server.

## [Sample Deployment Diagram](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#sample-deployment-diagram)

## [System Requirements](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#system-requirements)

The following systems are required to set up MetaDefender ICAP Server with an F5 BIG IP

- F5 BIG IP with ASM
- MetaDefender ICAP Server
- MetaDefender Core

## [Configuring MetaDefender ICAP Server](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-metadefender-icap-server)

For installation and configuration quick guidelines see: 1. Quick Start with MetaDefender ICAP Server.

For detailed instructions see 2. Installing or Upgrading MetaDefender ICAP Server and [3. Configuring MetaDefender ICAP Server](/docs/mdicap/v5.15.0/configuration/metadefender-icap-server-configuration).

### [Note on MetaDefender ICAP Server Licensing](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#note-on-metadefender-icap-server-licensing)

MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [2.4. MetaDefender ICAP Server Licensing](/docs/mdicap/v5.15.0/installation/metadefender-icap-server-licensing).

## [Configuring the F5 BIG IP Appliance](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-the-f5-big-ip-appliance)

The following configuration steps should be done from the F5 BIG IP Management Console interface. The steps below describe the minimum configuration required for MetaDefender ICAP Server integration with F5 BIG IP. Please refer to [Configuring BIG-IP ASM antivirus protection](https://support.f5.com/csp/article/K70941653) for a more advanced configuration.

Open a web browser and load the BIG IP Management Console. (Please refer to the BIG IP manual for details about how to open the BIG IP Management Console.)

This guide was written with a presumption that there is an already existing Virtual Server with an active Security Policy in the BIG IP ASM which we would like to protect against viruses.

### [Configuring the ICAP server](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-the-icap-server)

1. Navigate to **Security** > **Options** > **Application Security** > **Integrated Services** > **Anti-Virus Protection**.
2. Enter the ICAP server hostname or IP address in the **Server Host Name/IP Address** field.
3. Enter the ICAP server port in the **Server Port Number** field or leave the default value of 1344.
4. Select the **Guarantee Enforcement** option if you want the system to perform virus checking even if performing checking may slow your web application.
5. Click **Save**.
6. To activate the security policy changes immediately, click **Apply Policy**.

### [Configuring the antivirus blocking settings](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-the-antivirus-blocking-settings)

The information here is applicable for BIG-IP version 13.x. For other versions please check [Configuring BIG-IP ASM antivirus protection](https://support.f5.com/csp/article/K70941653).

1. Navigate to **Security** > **Application Security** > **Policy Building** > **Learning and Blocking Settings** > **Advanced Configuration**.
2. Expand **Antivirus Protection** and select either or both of the **Alarm** and **Block** check boxes for the **Virus Detected** violation.
3. Click **Save**.
4. To activate the security policy changes immediately, click **Apply Policy**.

### [Configuring the internal system variables](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-the-internal-system-variables)

You can configure the ICAP URI and the virus header name settings on the **System Variables** page in the Configuration utility. MetaDefender ICAP Server works with the default values out of the box so you don't need to configure them. If you would like to configure them anyway just follow these steps:

1. Navigate to **Security** > **Options** > **Application Security** > **Advanced Configuration** > **System Variables**.
2. For the **icap_uri** setting, enter the URI for the ICAP service, which checks requests for viruses by connecting to ICAP server. You can keep the default value ("/reqmod") for MetaDefender ICAP Server.
3. For the **virus_header_name** setting, enter the header name used by an anti-virus program on an ICAP server. For MetaDefender ICAP Server the default headers (X-Virus-Name, X-Infection-Found) can be used as it supports X-Infection-Found. [Here](/docs/mdicap/v5.15.0/operating/icap-response-headers) you can find the headers supported by MetaDefender ICAP Server.
4. Click Save.

### [Configuring antivirus scanning for HTTP file uploads and SOAP attachments](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-antivirus-scanning-for-http-file-uploads-and-soap-attachments)

1. Navigate to **Security** > **Application Security** > **Integrated Services** > **Anti-Virus Protection**.
2. Select the relevant security policy from the list
3. Click the **Inspect file uploads within HTTP requests** check box.
4. To perform antivirus scanning on SOAP attachments, move the relevant XML profiles from the **Antivirus Protection Disabled** list to the **Antivirus Protection Enabled** list.
5. Click **Save**.
6. To activate the security policy changes immediately, click **Apply Policy**.

### [Configuring the virtual server to use Application Security](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#configuring-the-virtual-server-to-use-application-security)

1. Navigate to **Local Traffic** > **Virtual Servers** > **Virtual Server List** > **Choose your virtual server that needs to use ICAP**.
2. Navigate **Security** tab > Choose **Policies**
3. Enable **Application Security Policy > Choose the Test_policy**

## [Testing the configuration](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#testing-the-configuration)

After you have finished the steps above your web application should be protected against malicious file uploads. To check this navigate to a page in your application where you can upload files and try to upload an [eicar](http://www.eicar.org/) test file.

For example a really simple file upload application could look like this:

When trying to submit the file upload the request will be blocked and the default block page will be displayed which should look like this:

For configuring the block page please refer to [Configuring what happens if a request is blocked](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/asm-implementations-13-1-0/27.html).

You can also check the [ICAP history](/docs/mdicap/v5.15.0/operating/icap-dashboard) to see that the processing took place:

### [Viewing reports for anti-virus detection](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#viewing-reports-for-anti-virus-detection)

To view reports of virus transactions detected by the ASM system, perform the following steps:

1. Navigate to **Security** > **Reporting** > **Applications** > **Charts**.
2. Select **Top Viruses Detected** from the drop down menu.
3. The system displays the detected viruses over time.

## [Limitations](/docs/mdicap/v5.15.0/integrations/f5-big-ip-asm--waf-#limitations)

Note

Due to limitations in F5 BIG IP ASM, OPSWAT Deep CDR will be unable to operate with full functionality.

MetaDefender ICAP Server will provide the sanitized files back to BIG IP ASM, but these sanitized files are ignored by ASM. If the request is allowed, then the original content is released by ASM.
