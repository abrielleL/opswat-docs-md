<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/saml-sso -->

# SAML SSO

My OPSWAT Central Mangement integrates with a third-party Single Sign-on Service (SSO), enabling Administrators to configure end-user authentication via multiple Identity Providers (IdP).

## How to configure on My OPSWAT Central Management console

### Setup SSO - End User Authentication

To integrate **My OPSWAT Central Mangement** with your own SSO service,

1. Log into the **My OPSWAT Central Mangement** console with admin permissions
2. Navigate to User Management > SSO > End User Authentication
3. On the Console tab, enable "Enable Single Sign On"
4. Enter an IdP Name. This is for your reference
5. Click the **Choose File** button to upload an IdP X.509 certificate .pem file that you got from the Identity Provider.
6. Enter Issuer you got earlier from the identity provider
7. Enter the IdP SSO URL you got earlier from the identity provider
8. Enter the IdP Log out URL and Error URL you got earlier from the identity provider if any
9. Click the **Save** button.

You can find detailed setup guideline for some identity providers below:

[Setup SSO with Okta](https://docs.opswat.com/macloud-sdp/secure-access/provision-users-through-your-okta)

[Setup SSO with Microsoft Azure](https://docs.opswat.com/macloud-sdp/secure-access/provision-users-through-your-microsoft-azure)

[Setup SSO with JumpCloud](https://docs.opswat.com/macloud-sdp/secure-access/provision-users-through-your-jumpcloud)

### Configure Access Rules

To configure Access Rules for Network Vendors that support DNAT (ex: Aruba), perform the below steps:

1. On the **Access Profiles** tab, create an Access Profile for Captive Portal
2. On **Aruba** dropdown, declare a value (ex: **ORG_B_2024RDR**) for Aruba-User-Role attributes

![](https://uploads.developerhub.io/prod/97qW/n1myl33na2742509ih56up343wucn1c8e6sthav4g6vrfr0jaga4uevs4bnew8vc.png)

3. Set up a rule for BYOD, Guest devices using devices’ authentication status condition

## How to configure on Aruba

1. On the Network Vendor (ex: Aruba) console, create an ACL (Network Access Control List) to forward traffic to your Captive portal server.

![](https://uploads.developerhub.io/prod/97qW/y6y9nv4ch0bxqwnyan5he1hj601v4n4fduyjmu4g6yjtfvttwdahyxgujbb0pmio.png)

**How to verify**:

1. Using a test device & Connect to the Network
2. If the Device's authentication status is **Unauthenticated** via the authentication method **SAML SSO,** it will match the **Unauthenticated Device Rule** above and the user will be redirected to the Captive Portal pages
3. Grant access using Single-sign options
4. After the authorization flow, the device should be switched to the correct VLAN
5. Confirm with Admin using RADIUS Events
