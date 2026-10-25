<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/fortigate -->

# FortiGate

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This documentation is based on FortiGate 5.4.3 documentation using web-based manager and CLI. For different version of FortiGate or missing information, refer to FortiGate user guides.

## [Configuration via Web-Based Manager](/docs/mdicap/v5.15.0/integrations/fortigate#configuration-via-web-based-manager)

### [Enabling ICAP feature](/docs/mdicap/v5.15.0/integrations/fortigate#enabling-icap-feature)

ICAP does not appear by default in the web-based manager, it has to be enabled by going to **System → Feature Select** and enabling **ICAP**. You may need to refresh the page in order to see the changes.

### [Adding ICAP server and profile](/docs/mdicap/v5.15.0/integrations/fortigate#adding-icap-server-and-profile)

1. Add ICAP server

   1. Select **Security Profiles → ICAP Servers**.
   2. Create new or edit an existing entry.

      1. The IP address and port should be the ones used by MetaDefender ICAP Server

2. Add ICAP profile

   1. Select **Security Profiles → ICAP**.
   2. Create new or edit an existing entry.
   3. Select the '**Enable Request Processing**' check-box, select your server's name from the drop-down list and in the '**Path**' field, type in '*OMSScanReq-AV*'.
   4. Select the '**Enable Response Processing**' check-box, select your server's name from the drop-down list and in the '**Path**' field, type in '*OMSScanResp-AV*'.
   5. Apply the changes.

3. Apply the ICAP profile in your policy/policies

   1. Select **Policy&Objects → IPv4 Policy | Explicit Proxy Policy**.
   2. Create new or edit an existing policy
   3. In the section '**Security Profiles**', switch on ICAP and select the previously created profile.

## [Configuration via CLI](/docs/mdicap/v5.15.0/integrations/fortigate#configuration-via-cli)

1. Add ICAP server

Add ICAP server via CLI
config icap server
edit <icap_server_name>
set ip-version {4 | 6} [default: 4]
set ip-address <server_ipv4>
set ip6-address <server_ipv6>
set max-connections <int> [default: 100]
set port <port_int> [default: 1344]
end

The example shown above in the web-based manager would look like this in the CLI:

Add concrate ICAP server via CLI
config icap server
edit my_icap_server
set ip-address 172.16.201.36
end

2. Add ICAP profile

Add ICAP profile via CLI
config icap profile
edit <icap_profile_name>
set replacemsg-group <grp_name>
set request {enable | disable}
[The following commands are enabled if request is set to 'enable']
set request-failure {error | bypass}
set request-path <path>
set request-server <icap_server>
set response {enable | disable}
[The following commands are enabled if response is set to 'enable']
set response-failure {error | bypass}
set response-path <path>
set response-server <icap_server>
set streaming-content-bypass {enable | disable}
end

The example shown above in the web-based manager would look like this in the CLI:

Add concrate ICAP profile via CLI
config icap profile
edit my_icap_profile
set request enable
set request-failure error
set request-path OMSScanReq-AV
set request-server my_icap_server
set response enable
set response-failure error
set response-path OMSScanResp-AV
set response-server my_icap_server
set streaming-content-bypass disable
end

3. Apply the ICAP profile policy (policy can be replaced by explicit-proxy-policy when setting ICAP for an Explicit Proxy Policy)

Apply ICAP profile via CLI
config firewall policy [or policy6 if IPv6 is used]
edit <index_int>
set icap-profile <icap_profile_name>
end

The example shown above in the web-based manager would look like this in the CLI:

Apply concrate ICAP profile via CLI
config firewall policy
edit 1
set icap-profile my_icap_profile
end

If you want to disable the ICAP profile for a given policy you should write

Disable ICAP profile via CLI
config firewall policy [or policy6 if IPv6 is used]
edit <index_int>
set icap-profile ""
end
## [Scanning HTTPS content](/docs/mdicap/v5.15.0/integrations/fortigate#scanning-https-content)

To be able to inspect and scan SSL/SSH traffic you have to enable it in Fortigate. After enabling this option you should download the certificate used by Fortigate and install/import it to the browsers which communicate with Fortigate. Otherwise you might see SSL/security related notifications or errors, or even not working web pages.

The certificate can be downloaded under **Security Profiles→ SSL/SSH Inspection**

## [Enable SSL inception via GUI](/docs/mdicap/v5.15.0/integrations/fortigate#enable-ssl-inception-via-gui)

1. Navigate to **Policy&Objects** and select the policy you would like to enable SSL inception to (for example an Explicit Proxy Policy)

2. In the **Edit** page of the selected policy locate the **Security Profiles** section
3. Turn **SSL/SSH Inspection** on and set it to **deep-inspection**

## [Enable SSL inspection via CLI](/docs/mdicap/v5.15.0/integrations/fortigate#enable-ssl-inspection-via-cli)

The steps shown above would like this via CLI:

Apply deep ssl inspection to an Explicit Proxy Policy
config firewall explicit-proxy-policy
edit 1
set ssl-ssh-profile deep-inspection
end
## [Resources](/docs/mdicap/v5.15.0/integrations/fortigate#resources)

- [Other FortiGate documentation](http://docs.fortinet.com/)
- [FortiOS Handbook - The Complete Guide to FortiOS](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-beta)
- [FortiOS 5.4.1 CLI Reference](http://docs.fortinet.com/d/fortigate-fortios-5.4-cli-reference)
