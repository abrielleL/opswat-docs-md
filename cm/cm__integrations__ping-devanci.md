<!-- source: https://www.opswat.com/docs/cm/integrations/ping-devanci -->

# Ping DaVinci

Ping Identity and OPSWAT have collaborated on an [DaVinci](https://www.pingidentity.com/en/pingone/davinci.html) Connector that permits an authentication flow to check a device’s compliance using My OPSWAT Central Management.  This is a different integration approach than outlined [PingOne IdP with Salesforce](https://www.opswat.com/docs/cm/secure-access-solution/pingone-idp-with-salesforce), which uses My OPSWAT Central Management’s ability to be in the SAML authentication flow of an IdP like PingFederation.

This integration approach, leveraging DaVinci, is easier to integrate than the SAML IdP approach as there is no need to understand the SAML protocol and cross integrate the IdP with My OPSWAT Central Management.  As described below, within DaVinci, as a result of the collaboration between OPSWAT and PingIdentity, you will find a pre-built Connector for My OPSWAT Central Management that is easy to add to a flow. You can find details [here](https://support.pingidentity.com/s/marketplace-integration-home-page).

The following describes how to prepare My OPSWAT Central Management for the DaVinci integration, and then details how to configure the DaVinci flow to call to My OPSWAT Central Management.

## Preparing My OPSWAT Central Management

Below are the provided steps for establishing Ping DaVinci with My OPSWAT Central Management

- Sign up for an account on My OPSWAT Central Management
- Create an application on My OPSWAT Central Management OAuth portal to get client key and client secret.
  - Navigate to the OAuth Application Portal: My OPSWAT Central Management
  - Create an OAuth Application for Ping DaVinci:

![](https://uploads.developerhub.io/prod/97qW/6qqfwblk64x53wbdmbtch1jprrb84ib5kl8tjkz1sxrvn33xycer51hnymjdskmi.jpg)

- Enable Cross-domain API settings, in **Settings > Integrations**, on your My OPSWAT Central Management account.

![](https://uploads.developerhub.io/prod/97qW/zpxpgy934qvrt6h8h6z1bsx87ffnoqss663lj3s93pqc1n1vs9bc5d846dz983ii.jpg)

- Client key and secret, from the My OPSWAT Central Management OAuth Settings Portal, will be required when configuring the Davinci Connector

![](https://uploads.developerhub.io/prod/97qW/4fxavadd43wbnl9lw3pc1nwxwzs0t1w5dj12i7z1nowcbly4xys341bzk5h242gj.jpg)

## Configuring the DaVinci Flow

- Input your My OPSWAT Central Management settings to your Connector configuration:

![](https://uploads.developerhub.io/prod/97qW/7xfy5yatb69xyp5xyyne3sf5evm6ysonsd3w4l9ivx5odlaud76m4kcwwgofblem.jpg)

- DaVinci Connector Settings:
  - Oauth Client Key and Oauth Client Secret of the app they created on My OPSWAT Central Management Oauth Portal.
  - My OPSWAT Central Management Domain where they set up their account, for example: [gears.opswat.com](http://metaaccess.opswat.com/).
  - Cross-domain API Port which they configured on My OPSWAT Central Management console if your solution uses cross-domain API to query device id.
