<!-- source: https://www.opswat.com/docs/cm/integrations/accounts -->

# Accounts

OPSWAT Add-on for Splunk supports multiple accounts and the user needs to select an appropriate account when creating a new input.

Follow the steps below to configure an account:

1. Login to Splunk Web UI.
2. Go to the **Configuration** page of OPSWAT Add-on for Splunk.
3. Click on the Account tab and start adding account details
4. Fill in required information.

| **Input Name** | **Required** | **Description** |
| ---- | ---- | ---- |
| Account Name | Yes | Any identifiable, unique name for the OPSWAT Account. This box will not accept the space in name |
| Host | Yes | OPSWAT Server DNS name or IP Address. Make sure it’s reachable from your Splunk Heavy Forwarder |
| OAuth Token Endpoint | Yes | OAuth token endpoint with default value “/o/oauth/token”. User can change it if the endpoint gets changed/updated anytime in the future. |
| Client Key | Yes | Client Key from an OAuth application you registered on My OPSWAT Central Management oAuth Portal* |
| Client Secret | Yes | Client Secret from an OAuth application you registered on My OPSWAT Central Management oAuth Portal* |

![](https://uploads.developerhub.io/prod/97qW/hm1yk96u80xf69sjnjrp82c4d6e5o0kwquy0ydmrxe4ur54cytkolgajrjpinfvw.png)
