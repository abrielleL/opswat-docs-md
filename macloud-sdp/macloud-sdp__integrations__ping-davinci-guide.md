<!-- source: https://www.opswat.com/docs/macloud-sdp/integrations/ping-davinci-guide -->

# PingOne DaVinci Guide

Ping Identity and OPSWAT have collaborated on an [DaVinci](https://www.pingidentity.com/en/pingone/davinci.html) Connector that permits an authentication flow to check a device’s compliance using MetaAccess. This is a different integration approach than outlined [here](https://docs.opswat.com/macloud-sdp/3.18.0/secure-access/pingone-idp-with-salesforce), which uses MetaDefender IT-OT Access’ ability to be in the SAML authentication flow of an IdP like PingFederation. This integration approach, leveraging DaVinci, is easier to integrate than the SAML IdP approach as there is no need to understand the SAML protocol and cross integrate the IdP with MetaDefender IT-OT Access. As described below, within DaVinci, as a result of the collaboration between OPSWAT and PingIdentity, you will find a pre-built Connector for MetaDefender IT-OT Access that is easy to add to a flow. You can find details [here](https://support.pingidentity.com/s/marketplace-integration-home-page).

The following describes how to prepare MetaDefender IT-OT Access for the DaVinci integration, and then details how to configure the DaVinci flow to call to MetaDefender IT-OT Access.

## [Preparing MetaDefender IT-OT Access](/docs/macloud-sdp/integrations/ping-davinci-guide#preparing-metadefender-it-ot-access)

Below are the provided steps for establishing Ping DaVinci with MetaDefender IT-OT Access

- Sign up for an account on OPSWAT MetaDefender IT-OT Access
- Create an application on MetaDefender IT-OT Access OAuth portal to get client key and client secret.

  - Navigate to the OAuth Application Portal: [MetaDefender IT-OT Access](https://metaaccess.opswat.com/o)
  - Create an OAuth Application for Ping DaVinci:

- Enable Cross-domain API settings, in **Settings > Integrations**, on your MetaDefender IT-OT Access account.

- Client key and secret, from the MetaDefender IT-OT Access OAuth Settings Portal, will be required when configuring the Davinci Connector

## [Configuring the DaVinci Flow](/docs/macloud-sdp/integrations/ping-davinci-guide#configuring-the-davinci-flow)

- Input your MetaDefender IT-OT Access settings to your Connector configuration:

- DaVinci Connector Settings:

  - Oauth Client Key and Oauth Client Secret of the app they created on MetaDefender IT-OT Access Oauth Portal.
  - MetaDefender IT-OT Access Domain where they set up their account, for example: [gears.opswat.com](http://metaaccess.opswat.com/).
  - Cross-domain API Port which they configured on MetaDefender IT-OT Access console if your solution uses cross-domain API to query device id.
