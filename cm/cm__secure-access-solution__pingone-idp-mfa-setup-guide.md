<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/pingone-idp-mfa-setup-guide -->

# PingOne IdP MFA Setup Guide

## How does it work?

In this setup guide, the authentication process will have 3 steps:

- Step 1: User enters the account credential
- Step 2: User enters the authentication code from the Authenticator App
- Step 3: Run a device posture check on the user's device

Administrators also can customize the Secure Access rules.

Notes: The IdP MFA method will apply to all applications on IT Access Secure Access Rules. To apply IdP MFA for specific applications, you must assign applications from Ping Console. More detail is in step "15. Assign Policy to Selected Applications"

![](https://uploads.developerhub.io/prod/97qW/y7hab8fgcb1frr4gxqk7dro64ulb4znkgx5l5oi8z2vvu8lh6ozmw0pbkct731yk.png)

## Setup guide

1. In My OPSWAT Central Management, navigate to Secure Access > Access Methods > IdP MFA, and Enable IdP MFA

![](https://uploads.developerhub.io/prod/97qW/pjo1p8h9jttqmn2gu277sj5rn8acgvjpgqyl6vegg1x2pan5cbky60jr5j87fv67.png)

2. Then download **IdP Metadata (XML)** file
3. In PingIdentity, go to “Integrations > External Idps“, then click on Add Provider![](https://uploads.developerhub.io/prod/1yda/09l9yolwgp4miec28vkmqaw3rnsm44np2dj2rke7z721xjws0qkyhm2zn4mnw5ru.png)
4. Select **SAML**, and filling information![](https://uploads.developerhub.io/prod/1yda/yso30omieo9x0m3ufzlbwuuqf4cee2aevsbckqtkgjsfsnlb7awsay28n7uu70hl.png)
5. Choose Signing Certificate and check on "Sign Authn Request"![](https://uploads.developerhub.io/prod/1yda/2h86nctt68fjy1gtpjqdg4zdhbuaj95dek5difmhdafu9c603axt4qnt0o2n6per.png)
6. Import Metadata downloaded in Step 2, and select "HTTP POST" as SSO Binding![](https://uploads.developerhub.io/prod/1yda/w636mr6v12w2eqgo05ki2l9lz39ox1pwf4oqbv743plmvkrt13wd5w0el7p9tcq5.png)![](https://uploads.developerhub.io/prod/1yda/usov1q33n8kot0aunzterayk3yczimi24lxidaee3m8r102lg05wr3gg94lrvfw9.png)
7. Click on **Save & Finish** ![](https://uploads.developerhub.io/prod/1yda/vd4e2vtfxb9welqx1d7gwcidddq06c36zeufk69egbg55xwvctf7x6qx9s4u56mc.png)
8. Enabled the new IDP ![](https://uploads.developerhub.io/prod/1yda/oczhdxqbiliokfnpvz08190dw69hn9orlfwo4p3h2ghh55er2j2dyz0c1gjz8p5g.png)
9. From the new created IDP, click on the pencil icon, then click on IDP Configuration tab and click to download the metadata ![](https://uploads.developerhub.io/prod/1yda/6y3spwv72q5vemqzpcfiwyd6tqdqg6qscwmn0rwk31t332aiitkk3emj7e6wozew.png)
10. Upload the Ping Metadata in My OPSWAT Central Management and **Save** ![](https://uploads.developerhub.io/prod/1yda/qhkjsnfcrnk02zk0x1390t1jeu6x13aorlsmxjz1bao7oujgbuk2ga7ittqyx1it.png)
11. In PingIdentity, go to Authentication > Authentication, click on **Add Policy** button and fill information ![](https://uploads.developerhub.io/prod/1yda/emnhiy323ajo8lrlh5ohbpsyhokegz22z9tddbkujqf5x3wwirn103zn25g18w4j.png) ![](https://uploads.developerhub.io/prod/1yda/6pvaswlaq4iusoxswqa7ifd81rue1nyvy1yqq4wkcny1tqypg3papax1lmrbrp8d.png)
12. Add Login as first step then click on **Add step** for next step ![](https://uploads.developerhub.io/prod/1yda/efgcwex6fhg5dwvhyprnkcbllsfhu6ujiwt0otbaxc4quup00ldb3jpb4ajjbg1q.png)
13. (Optional) Select Multi-factor Authentication as second step and click on **Add step** ![](https://uploads.developerhub.io/prod/1yda/riqhudf58271wk686gymvtep23ejdduni5tt0jmgneuz5f4hn6hq32jdy1oh41kz.png)
14. Select **External Identity Provider** then select the new IDP for **External Identity Provider** then check on the box **Pass user context to provider**![](https://uploads.developerhub.io/prod/1yda/ep2dojzcz7bz43f09hyqljljpxvt4qhf642bwk35ps9z6uvm1khj0fw0stfhqjxp.png)
15. Assign Policy to Selected Applications.

Navigate to Applications. Add the policy to selected applications

![](https://uploads.developerhub.io/prod/97qW/fuqh57jdwgo69vo76agesuyincqem9oj922ljb1yr9hhhx5snjsfzqksu39m3h5m.png)

16. Test the integration
