<!-- source: https://www.opswat.com/docs/mdicap/integrations/f5-big-ip-ltm -->

# F5 BIG IP LTM

MetaDefender Core –via MetaDefender ICAP Server– can be used to scan and sanitize all files being uploaded to the F5 BIG IP server with all of the engines in MetaDefender Core to make sure that no malware is able to get to the web servers behind the Big IP server. This guide describes the basic steps to getting MetaDefender ICAP Server working with your F5 BIG IP server.

Info

The simplest way to integrate MetaDefender ICAP Server with F5 BIG IP is to use the iApps framework of F5.

The iApps technology was released in F5’s v11, so the description in this page is more generic.

For details about the MetaDefender ICAP Server iApp template and how to use it, see [4.4.3.6 ICAP Server iApp template](/docs/mdicap/integrations/icap-server-iapp-template).

## [Sample Deployment Diagram](/docs/mdicap/integrations/f5-big-ip-ltm#sample-deployment-diagram)

## [System Requirements](/docs/mdicap/integrations/f5-big-ip-ltm#system-requirements)

The following systems are required to set up MetaDefender ICAP Server with an F5 BIG IP

- F5 BIG IP with LTM
- MetaDefender ICAP Server
- MetaDefender Core

## [Deployment ‘How To’ Video](/docs/mdicap/integrations/f5-big-ip-ltm#deployment-how-to-video)

To help you get up and running quickly, watch this video that demonstrates how to integrate MetaDefender ICAP Server with F5® BIG-IP® Load Traffic Manager™ (LTM®): <https://www.opswat.com/videos/how-to-integrate-metadefender-icap-with-f5>

## [Configuring MetaDefender ICAP Server](/docs/mdicap/integrations/f5-big-ip-ltm#configuring-metadefender-icap-server)

For installation and configuration quick guidelines see: 1. Quick Start with MetaDefender ICAP Server.

For detailed instructions see 2. Installing or Upgrading MetaDefender ICAP Server and [3. Configuring MetaDefender ICAP Server](/docs/mdicap/configuration/metadefender-icap-server-configuration).

### [Note on MetaDefender ICAP Server Licensing](/docs/mdicap/integrations/f5-big-ip-ltm#note-on-metadefender-icap-server-licensing)

MetaDefender ICAP Server must have a valid license to function correctly. For license configuration details see [2.4. MetaDefender ICAP Server Licensing](/docs/mdicap/installation/metadefender-icap-server-licensing).

## [Configuring the F5 BIG IP Appliance](/docs/mdicap/integrations/f5-big-ip-ltm#configuring-the-f5-big-ip-appliance)

The following configuration steps should be done from the F5 BIG IP Management Console interface. The steps below describe the minimum configuration required for MetaDefender ICAP Server integration with F5 BIG IP. Please refer to the [F5 BIG IP manual for advanced configuration](https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/12.html).

1. Open a web browser and load the BIG IP Management Console. (Please refer to the BIG IP manual for details about how to open the BIG IP Management Console.)

### [Creating a custom client-side ICAP profile](/docs/mdicap/integrations/f5-big-ip-ltm#creating-a-custom-client-side-icap-profile)

You create this ICAP profile when you want to use an ICAP server to wrap an HTTP request in an ICAP message before the BIG-IP system sends the request to a pool of web servers. The profile specifies the HTTP request-header values that the ICAP server uses for the ICAP message.Important: You can use macro expansion for all ICAP header values. For example, if an ICAP header value contains ${SERVER_IP}, the BIG-IP system replaces the macro with the IP address of the ICAP server selected from the pool assigned to the internal virtual server. If an ICAP header value contains ${SERVER_PORT}, the BIG-IP system replaces the macro with the port of the ICAP server selected from the pool assigned to the internal virtual server. For example, you can set the URI value in an ICAP profile to icap://${SERVER_IP}:${SERVER_PORT}/OMSScanReq-AV.

1. On the Main tab, click Local Traffic > Profiles > Services > ICAP.

2. Click Create.
3. In the Name field, type a unique name for the profile.
4. For the Parent Profile setting, retain the default value, icap.
5. On the right side of the screen, select the Custom check box.
6. In the URI field, type a URI in this format: icap://hostname:port/path. For example, using macro expansion, you can set the URI value to:icap://${SERVER_IP}:${SERVER_PORT}/OMSScanReq-AV .
7. In the Preview Length field, type a length or retain the default value 0. This value defines the amount of the HTTP request or response that the BIG-IP system offers to the ICAP server when sending the request or response to the server for adaptation. This value should not exceed the length of the preview that the ICAP server has indicated it will accept.
8. Leave empty for "Header From", "Host", "Referer", "User Agent" fields.

9. Click Finished.

After you create the ICAP profile, you can assign it to an internal virtual server so that the HTTP request that the BIG-IP system sends to an ICAP server is wrapped in an ICAP message, according to the settings you specified in the ICAP profile.

### [Creating a pool of ICAP servers](/docs/mdicap/integrations/f5-big-ip-ltm#creating-a-pool-of-icap-servers)

You perform this task to create a pool of ICAP servers that perform content adaptation on HTTP requests.

1. On the Main tab, click Local Traffic > Pools. The Pool List screen opens.
2. Click Create. The New Pool screen opens.
3. In the Name field, type a unique name for the pool.
4. For the Health Monitors setting, from the Available list, select a monitor other than http(s), and click << to move the monitor to the Active list.
5. From the Load Balancing Method list, select how the system distributes traffic to members of this pool. The default is Round Robin.
6. For the Priority Group Activation setting, specify how to handle priority groups:

   - Select Disabled to disable priority groups. This is the default option.
   - Select Less than, and in the Available Members field type the minimum number of members that must remain available in each priority group in order for traffic to remain confined to that group.
7. Using the New Members setting, add each resource that you want to include in the pool:

   1. Either type an IP address in the Address field, or select a node address from the Node List.
   2. Type a port number in the Service Port field, or select a service name from the list.
   3. To specify a priority group, type a priority number in the Priority field.
   4. Click Add.
8. Click Finished.

The pool of ICAP load balancing servers appears in the Pools list.

### [Creating an internal virtual server for forwarding requests to an ICAP server](/docs/mdicap/integrations/f5-big-ip-ltm#creating-an-internal-virtual-server-for-forwarding-requests-to-an-icap-server)

A virtual server of type internal provides a destination that a standard type of virtual server can use when forwarding HTTP requests slated for ICAP-based content adaptation.

1. On the Main tab, click Local Traffic > Virtual Servers. The Virtual Server List screen opens.
2. Click the Create button. The New Virtual Server screen opens.
3. In the Name field, type a unique name for the virtual server.
4. In the Description field, type a description of the virtual server. For example: This virtual server ensures HTTP request modification through the use of the service_name ICAP service..
5. From the Type list, select Internal.
6. For the State setting, verify that the value is set to Enabled.
7. From the Configuration list, select Advanced.
8. From the ICAP Profile list, select the ICAP profile that you previously created for handling HTTP requests.
9. From the Default Pool list, select the pool of ICAP servers that you previously created.
10. Click Finished.

After you perform this task, a standard type of virtual server can forward HTTP requests to an internal type of virtual server. The internal virtual server then sends the request to a pool of ICAP servers, before sending the request back to the standard virtual server for forwarding to the pool of web servers.

### [Creating a custom Request Adapt profile](/docs/mdicap/integrations/f5-big-ip-ltm#creating-a-custom-request-adapt-profile)

You create a Request Adapt type of profile when you want a standard HTTP virtual server to forward HTTP requests to an internal virtual server that references a pool of ICAP servers. A Request Adapt type of profile instructs the HTTP virtual server to send an HTTP request to a named internal virtual server for possible request modification.

1. On the Main tab, click Local Traffic > Profiles > Services > Request Adapt.
2. Click Create.
3. In the Name field, type a unique name for the profile.
4. For the Parent Profile setting, retain the default value, requestadapt.
5. On the right side of the screen, click the Custom check box.
6. For the Enabled setting, retain the default value, Enabled. When you set this value to Enabled, the BIG-IP system forwards HTTP requests to the specified internal virtual server for adaptation.
7. From the Internal Virtual Name list, select the name of the internal virtual server that you previously created for forwarding HTTP requests to the pool of iCAP servers.
8. In the Preview Size field, type a numeric value. This specifies the maximum size of the preview buffer. This buffer holds a copy of the HTTP request header and the data sent to the internal virtual server, in case the adaptation server reports that no adaptation is needed. Setting the preview size to 0 disables buffering of the request and should only be done if the adaptation server always returns a modified HTTP request or the original HTTP request.
9. In the Timeout field, type a numeric value, in seconds. If the internal virtual server does not return a result within the specified time, a timeout error occurs. To disable the timeout, use the value 0.
10. From the Service Down Action list, select an action for the BIG-IP system to take if the internal virtual server returns an error:

    - Select Ignore to instruct the BIG-IP system to ignore the error and send the unmodified HTTP request to an HTTP server in the HTTP server pool.
    - Select Drop to instruct the BIG-IP system to drop the connection.
    - Select Reset to instruct the BIG-IP system to reset the connection.
11. Click Finished.

After you perform this task, the BIG-IP system contains a Request Adapt profile that a standard HTTP virtual server can use to forward an HTTP request to an internal virtual server for ICAP traffic.

### [Creating a custom HTTP profile](/docs/mdicap/integrations/f5-big-ip-ltm#creating-a-custom-http-profile)

An HTTP profile defines the way that you want the BIG-IP®system to manage HTTP traffic.Note: Other HTTP profile types (HTTP Compression and Web Acceleration) enable you to configure compression and cache settings, as required. Use of these profile types is optional.

1. On the Main tab, click Local Traffic > Profiles > Services > HTTP. The HTTP profile list screen opens.
2. Click Create. The New HTTP Profile screen opens.
3. In the Name field, type a unique name for the profile.
4. From the Parent Profile list, select http.
5. Select the Custom check box.
6. Modify the settings, as required.
7. Click Finished.

The custom HTTP profile now appears in the HTTP profile list screen.

### [Creating a pool to process HTTP traffic](/docs/mdicap/integrations/f5-big-ip-ltm#creating-a-pool-to-process-http-traffic)

You can create a pool of web servers to process HTTP requests.

1. On the Main tab, click Local Traffic > Pools. The Pool List screen opens.
2. Click Create. The New Pool screen opens.
3. In the Name field, type a unique name for the pool.
4. For the Health Monitors setting, from the Available list, select a monitor other than http(s), and click << to move the monitor to the Active list.
5. From the Load Balancing Method list, select how the system distributes traffic to members of this pool. The default is Round Robin.
6. For the Priority Group Activation setting, specify how to handle priority groups:

   - Select Disabled to disable priority groups. This is the default option.
   - Select Less than, and in the Available Members field type the minimum number of members that must remain available in each priority group in order for traffic to remain confined to that group.
7. Using the New Members setting, add each resource that you want to include in the pool:

   1. Type an IP address in the Address field, or select a node address from the Node List.
   2. Type 80 in the Service Port field, or select HTTP from the list.
   3. (Optional) Type a priority number in the Priority field.
   4. Click Add.
8. Click Finished.

The new pool appears in the Pools list.

### [Creating an HTTP virtual server for enabling request adaptation](/docs/mdicap/integrations/f5-big-ip-ltm#creating-an-http-virtual-server-for-enabling-request-adaptation)

You perform this task to create a standard virtual server that can forward an HTTP request to an internal virtual server. The internal virtual server then sends the request to a pool of ICAP servers before the BIG-IP® system sends the request to the web server.

1. On the Main tab, click Local Traffic > Virtual Servers. The Virtual Server List screen opens.
2. Click the Create button. The New Virtual Server screen opens.
3. In the Name field, type a unique name for the virtual server.
4. For the Destination setting, in the Address field, type the IP address that you want to use as a destination for client traffic destined for a pool of HTTP web servers.The IP address you type must be available and not in the loopback network.
5. In the Service Port field, type 80, or select HTTP from the list.
6. From the Configuration list, select Advanced.
7. From the HTTP Profile list, select the name of the HTTP profile that you created previously.
8. From the Request Adapt Profile list, select the name of the Request Adapt profile that you previously created.
9. From the Source Address Translation list, select Auto Map.
10. From the Default Pool list, select the name of the HTTP server pool that you previously created.
11. Click Finished.

### [Configuring the REQMOD (Request Modification) service](/docs/mdicap/integrations/f5-big-ip-ltm#configuring-the-reqmod-request-modification-service)

In order to configure F5 BIG-IP LTM to only forward HTTP requests to the MetaDefender Core ICAP server, follow the steps described below. In the case you want to configure F5 BIG-IP LTM to forward both HTTP requests and responses, refer to the "Configuring REQMOD and RESPMOD Services" section.

1. Open a Web browser and follow the instructions from the page: <https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/12.html>
2. Update the REQMOD ICAP service profile.

   1. Go to “Local Traffic” > “Profiles” > “Services” > “ICAP”.
   2. In the list that appears select your ICAP Request mod service.
   3. Set “Preview Length” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.
3. Update the Request Adapt profile.

   1. Go to “Local Traffic” > “Profiles” > “Services” > “Request Adapt”.
   2. In the list that appears select your request adapt service.
   3. Set “Preview Size” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.

### [Configuring REQMOD and RESPMOD Services](/docs/mdicap/integrations/f5-big-ip-ltm#configuring-reqmod-and-respmod-services)

In order to configure F5 BIG-IP LTM to forward both HTTP requests and responses to the MetaDefender Core ICAP server, follow the steps described below. In the case you want to configure F5 BIG-IP LTM to only forward HTTP responses, refer to the "Configuring REQMOD Service" section.

1. Open a Web browser and follow the instructions from the page: <https://techdocs.f5.com/kb/en-us/products/big-ip_ltm/manuals/product/ltm-implementations-11-5-1/13.html>
2. Update your REQMOD ICAP service profile.

   1. Go to “Local Traffic” > “Profiles” > “Services” > “ICAP”.
   2. In the list that appears select your ICAP Request mod service.
   3. Set “Preview Length” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.
3. Update your RESPMOD ICAP service profile.

   1. Go back to “Local Traffic” > “Profiles” > “Services” > “ICAP”.
   2. In the list that appears select your ICAP Response mod service.
   3. Set “Preview Length” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.
4. Update your Request Adapt profile.

   1. Go to “Local Traffic” > “Profiles” > “Services” > “Request Adapt”.
   2. In the list that appears select your request adapt service.
   3. Set “Preview Size” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.
5. Update Response Adapt service profile (only if RESPMOD is used)

   1. Go to “Local Traffic” > “Profiles” > “Services” > “Response Adapt”.
   2. In the list that appears select your response adapt service.
   3. Set “Preview Size” to 0 and make sure the checkbox next to it is checked.
   4. Click “Update” to apply the changes.

### [Configuring Service Down Actions](/docs/mdicap/integrations/f5-big-ip-ltm#configuring-service-down-actions)

If you followed the steps described in "Configuring REQMOD Service" or "Configuring REQMOD and RESPMOD Services". Big-IP will be configured to drop all connections when the ICAP service is down.

F5 can be configured to forward HTTP data to the web server/web client in the case the ICAP server is unrechable. If you are using an ICAP server pool that contains more than one MetaDefender ICAP Server, F5 can also be configured to forward the HTTP content to a different pool member.

### [Bypass ICAP server on service down](/docs/mdicap/integrations/f5-big-ip-ltm#bypass-icap-server-on-service-down)

Note that bypassing ICAP on service down may lower your organisation's security as content will be forwarded without being scanned.

1. Open the “Request adapt” profile (“Profiles” > “Services” > “Request Adapt”)
2. Set “Service Down Action” to “Ignore”.
3. Click the "Update" button to apply the changes.

### [Transfer content to different pool member](/docs/mdicap/integrations/f5-big-ip-ltm#transfer-content-to-different-pool-member)

If you are using an ICAP server pool that contains more than one MetaDefender ICAP Server, you can also configure Big-IP to send the HTTP content to a different ICAP pool member.

1. Open your ICAP services pool properties ("Pools" > "Pool List").
2. Set the "Configuration" list to "Advanced".
3. Set the “Action on Service Down” property to “Reselect”.
4. Click the "Update" button to apply the changes

## [Throughput limitation by license](/docs/mdicap/integrations/f5-big-ip-ltm#throughput-limitation-by-license)

If you experience slow download/upload through F5 then there is a chance that your throughput is limited by F5 license.

How to check the maximum throughput allowed by license:

1. SSH into F5: On Windows open PuTTY then type the IP of the F5 device, and click Open

2. Use the default login: admin/admin
3. Type tmsh and press enter
4. Type "show /sys license detail | grep perf" to see performance limitations by license
5. To exit from tmsh type "quit" and press enter, to quit from PuTTY type "exit" then press enter
