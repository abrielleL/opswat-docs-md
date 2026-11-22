<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/saml-sso -->

# SAML SSO

My OPSWAT Central Management integrates with a third-party SAML Single Sign-On (SSO) service, enabling Administrators to authenticate NAC end users through their own Identity Provider (IdP).

## How to configure on My OPSWAT Central Management console

### Setup SSO - End User Authentication

1. Log into the **My OPSWAT Central Management** console with admin permissions
2. Navigate to RADIUS NAC > Captive Portal > SSO
3. Copy the ACS URL and Entity ID provided by NAC. You will need them to configure the Identity Provider
4. Click the **Choose File** button to import the IdP metadata file you got from the Identity Provider
5. Enter an IdP Name. This is for your reference
6. Click the **Save** button

## How to configure on Okta

1. On the Okta SAML application, select General > Edit SAML Settings
2. Check "Use this for Recipient URL and Destination URL"
3. Fill Single sign-on URL with the My OPSWAT Central Management ACS URL
4. Fill Audience URI (SP Entity ID) with the My OPSWAT Central Management Entity ID
5. Set Default RelayState to **source=agent**
6. Configure attribute mapping:
   1. On the SAML application, select the Sign On tab
   2. Scroll down to the Attribute statements section
   3. Click **Add Expression** and map the needed attributes. For example, if an Okta user has the profile attribute Organization = OPSWAT, map it to return the user's organization value
   4. To get the Okta user's group attributes (group name, group description), add them the same way
7. On the Assignments tab, assign the users or groups who can sign in
8. On the Sign On tab, download the IdP metadata file and import it into My OPSWAT Central Management

## Configure Access Rules

1. Navigate to RADIUS NAC > Rules and click **Add a new rule**
2. Set up a rule using the SSO user attributes mapped above as conditions (ex: Organization = OPSWAT, or a group name)
3. Select the access to grant, then click the **Save** button

For example, set up a rule that requires MFA for devices whose users sign in via SAML SSO.

**How to verify**:

1. Using a test device, connect to the network
2. Sign in using the Single Sign-On option with an assigned Okta user
3. After the authorization flow, the device should get the access set by the matching rule
4. Confirm with Admin using RADIUS Events

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
