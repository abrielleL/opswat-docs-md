<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/radius-server-authentication-mode-configuration -->

# RADIUS Server Authentication Mode Configuration

## [Accessing the RADIUS Server Interface](/docs/manac/nac-v8.1.1/configuration/radius-server-authentication-mode-configuration#accessing-the-radius-server-interface)

Login to the NAC management interface at: <https://portal.myweblogon.com:8443/manage>. If this does not work, you can replace ‘[portal.myweblogon.com](http://portal.myweblogon.com/)’ with the IP address of your NAC appliance. In a cluster environment, this must be the manager node. If a branded URL is configured, replace ‘[portal.myweblogon.com](http://portal.myweblogon.com/)’ with the branded URL chosen. Once Logged in, choose Configuration Manger > Enforcement Setup > RADIUS Configuration > RADIUS Configuration.

NAC provides three RADIUS server modes. Only one mode can be in use at a time. In most cases, Direct mode will be used, however, proxy and out-of-line modes provide powerful options for more advanced use-cases.

- **Direct Mode:** NAC performs all RADIUS authentication actions and communicates via RADIUS only with the access layer network infrastructure.
- **Proxy Mode:** NAC performs authorization level access and role enforcement, but forwards authentication requests to an upstream RADIUS server or servers. Proxy mode is best utilized in networks where functioning RADIUS infrastructure already exists, or there is a need to use multiple RADIUS servers for authenticating different classes of users. Note that in this mode, NAC will perform MAC authentication for open and PSK wireless networks and non-802.1x wired ports that are configured to use NAC for MAC authentication via RADIUS.
- **Out-of-Line Mode:** NAC will not be used for authentication, or authorization, but instead will be used to dynamically assign RADIUS attributes to perform policy enforcement. Note that NAC must still be a RADIUS accounting server and not all vendors are supported in this model.

Click below to find configuration guide for each mode mentioned above.

[Configure RADIUS Server for Direct Authentication](/docs/manac/nac-v8.1.1/configuration/configure-radius-server-for-direct-authentication)

[Configure RADIUS Server for Out-of-Line Mode](/docs/manac/nac-v8.1.1/configuration/configure-radius-server-for-out-of-line-mode)

[Configure RADIUS Server in for Proxy Mode](/docs/manac/nac-v8.1.1/configuration/configure-radius-server-in-for-proxy-mode)
