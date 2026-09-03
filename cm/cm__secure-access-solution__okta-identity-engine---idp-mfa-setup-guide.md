<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-identity-engine---idp-mfa-setup-guide -->

# Okta Identity Engine - IdP MFA Setup Guide

## Setup Steps

1. In My OPSWAT Central Management, navigate to Secure Access > Access Methods > IdP MFA, and Enable IdP MFA

![](https://uploads.developerhub.io/prod/97qW/znagyh5s8heojxg0biuf8an8r8iq56eh05sf74ge28rtwayzc1208d4byom9l5og.jpg)

2. Copy the Entity ID, Single Sign-On Url, and download the IdP Certificate. Then navigate to your Okta Administrator account.
3. In Okta Admin, go to “Security > Identity Providers“ to setup OPWAT’s Compliance-Based IdP MFA

![](https://uploads.developerhub.io/prod/97qW/7up56pehrrzwnk1rqguh63manabkdcbed18fy3zaihum9fe0uf0f00njbcdwxg2v.jpg)

4. Add Identity Provider, select “SAML 2.0 IdP“ and click "Next" button

![](https://uploads.developerhub.io/prod/97qW/85eb22ft08lwk6gyx4elpnji6penyfl62t1nfd5712q2lkzrq2t1uhgjbohrfrjd.png)

5. Fill in the information with the provided metadata from My OPSWAT Central Management

![](https://uploads.developerhub.io/prod/97qW/jwk2omecxgtvls69kag6s4pzaeyg5aeg7yi5pdr0fhgh2gnplb8b4gpe9sihir77.png)

6. Keep the default configurations in the Advanced Settings
7. Download the SAML metadata of the new IdP

![](https://uploads.developerhub.io/prod/97qW/qdei5t2y3a88bz88hgfc5hi33d9tkz3wc0y0nlso0ah3c3hr6ch6gpsbrqps0sye.)

_

8. **Upload** the Okta Metadata in My OPSWAT Central Management and **Save**

![](https://uploads.developerhub.io/prod/97qW/k8ltp6a4x2ax2snwr7gxcqohaciz9o165hmgajmxqp75ai3uu1hnsqydp9gpkxix.jpg)

![](https://uploads.developerhub.io/prod/97qW/emkw45wgbxpm0eo20rqx7p18j5x4wtrcwrhqj0gowmmxdb8ez8rsbgyuv8hlfxll.png)

9. In Okta, navigate to Security > Authenticators > Setup and click "Add authenticator"

![](https://uploads.developerhub.io/prod/97qW/uk4362sn7ani21idcgn0302o9bknv4ihgebq3enyc6o4fmn3rik8jmddv6cits0z.png)

![](https://uploads.developerhub.io/prod/97qW/z09or3mpcv8gj6qm8ev5i9tbm9ssqmicnkoh1gedl245mwrvy5exn8jul3nak1cm.png)

9. In the Security > Authenticators, select Enrollment tab and add a new My OPSWAT Central Management policy

- It's recommended to assign **none-admin** group in this policy before testing all the configuration and flow.
- Need to require "My OPSWAT Central Management (IdP)" and "Password" and disable other authenticators
- Keep the default rule

![](https://uploads.developerhub.io/prod/97qW/p8viym72ak46fe60n68pbpbfnpcjsb52jqrubsh7yj6biizgt3ec191kozn0oge4.png)

10. Configure your Global Session Policy.

- It's recommended to assign to a **none-admin group** before testing the flow and policy
- It's recommended to require MFA at every sign in $plugin[16ahuz7dkwj]

![](https://uploads.developerhub.io/prod/97qW/l14epq7r1mzo1gd5cnolweeumywddxdufmyhjlhoa6ii8v9m7gzf7demjyr9rxmo.png)

![](https://uploads.developerhub.io/prod/97qW/w18z4220nufg0u06t4bpkzsok292u4xkkrrlf3iincusfh1s14qmn4qcbqhq0klr.png)

11. Test your integration
