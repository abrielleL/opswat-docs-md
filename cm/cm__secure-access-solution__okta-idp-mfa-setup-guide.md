<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-idp-mfa-setup-guide -->

# Okta IdP MFA Setup Guide

## Setup Steps

1. In My OPSWAT Central Management, navigate to Secure Access > Access Methods > IdP MFA, and Enable IdP MFA

![](https://uploads.developerhub.io/prod/97qW/6x2sphjvo8fn62jz1mgdpxpdmo72lws7cd5vtu21gh1v50c44sf02kirow74upxg.png)

2. Copy the Entity ID, Single Sign-On Url, and download the IdP Certificate. Then navigate to your Okta Administrator account.
3. In Okta, go to “Identity Providers“ to setup OPWAT’s Compliance-Based IdP MFA

![](https://uploads.developerhub.io/prod/97qW/c5txhabi5pcpnrb4rkkfas5z9e40ncub0q1n1na9yuewckxyla43cn0y1gg0f09b.png)

4. Add Identity Provider, “Add SAML 2.0 IdP“

![](https://uploads.developerhub.io/prod/97qW/ijksg3rb1pxv0qbean7c2v9dx11sf9vl0ed7iv78cheetfn0hqj775delgdmm3oi.)

5. Fill in the information with the provided metadata from My OPSWAT Central Management

![](https://uploads.developerhub.io/prod/97qW/ow7a3ro8ccnv3y1trb65bbgfyh9u54h4s012lb6f744j9twui4zus0uvrxfqd3m8.)

6. Keep the default configurations in the Advanced Settings, then click “Add Identity Provider“

_

![](https://uploads.developerhub.io/prod/97qW/zzs0w45b96wg6w8zyol4ujx85nv40yt3hh5o59n688htqu7sddrjtjhjkc4mybqn.)

_

7. Download the SAML metadata of the new IdP

![](https://uploads.developerhub.io/prod/97qW/it1p7wpycvb9dugsvk6l2an3edzc2uravxlo8q7e221wfxmmvf9c4rx6j77pbo3t.)

_

8. **Upload** the Okta Metadata in My OPSWAT Central Management and **Save**

![](https://uploads.developerhub.io/prod/97qW/dmncjto3a86tg5ixrwl313psw95qxqlo004pyftugbkqnx8s9tw83vc0tkgrhnji.png)

8. In Okta, navigate to Multifactor and configure IdP Factor to use the newly setup IdP

![](https://uploads.developerhub.io/prod/97qW/p4rp6wt29e2yal1h5vaodh3mvcxbvopc7i2ivr09ekoqf1wykq1br8pli50jn1e5.png)

## Recommended Settings

It is recommended to enable IdP factor on every sign on attempt for your critical applications.

1. Inside the Okta admin panel, go to **Security** → **Multifactor**.
2. In the Mutlifactor page, open the Factor **Enrollment** tab, click **Add Multifactor Policy**
3. Create a Multifactor Policy with only the IdP Factor *Required* and all other factors *Disabled*
4. In the Multifactor page, make newly created Multifactor Policy the highest priority by moving the policy to the first position in the policy list

![](https://uploads.developerhub.io/prod/97qW/f8x85957s430r9tfge0li6p4a5tq6469socaos7drevlxwoedxroajo8f5d797da.PNG)

5. In the newly created Mutlifactor Policy, click the pencil icon on the Default rule.
6. In the Default rule dialog, select only **Applications** under “User is accessing” section.

![](https://uploads.developerhub.io/prod/97qW/2uzte2yyan3m7nksh6lswlx70qwe7swk6yntityxe8m1fce1mwd6agknasqhwf4e.png)

7. Back inside the Okta admin panel, go to your applications and select an application.
8. Select the **Sign On** tab
9. Scroll down to **Sign On Policy** and **Add Rule**

![](https://uploads.developerhub.io/prod/97qW/mk2qzkvm0c6r4zxv5fvnwv3uixz44pnlpcw7r7itqutnvaejiqv3mjrxgm2o79qt.png)

10. Configure your policy with the following **Access** settings, and **Save**

![](https://uploads.developerhub.io/prod/97qW/ablqbpln922y48oqdu91oephjz1rhf12t3dv28bjze6c4g46awia3goar42oanvn.png)

11. Your critical application is now configured to require IdP MFA on every sign on

![](https://uploads.developerhub.io/prod/97qW/xcvvlaao2jtxyzf95k7vn1fijbz2mlefrtue600hb1losbjvigy2au9x465zdxe0.png)
