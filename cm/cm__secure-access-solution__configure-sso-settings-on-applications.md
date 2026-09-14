<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configure-sso-settings-on-applications -->

# Configure SSO Settings on Applications

This step updates IdP certificate on single sign-on settings of your application in order to the application can verify user authentication results from My OPSWAT Central Management. Otherwise, the application couldn't trust the authentications and not let your end-user login.

1. Log into the My OPSWAT Central Management console, navigate to **Secure Access** > **Protected Apps**.
2. Select an application you would like to configure, select SSO Setup Instructions tab and click Download Certificate to download a self-signed certificate My OPSWAT Central Management generated for your account.

![](https://uploads.developerhub.io/prod/97qW/o8i9yus387ki5o97cn6rrg3lkb8iwprzagwbxnd0i4r4pfz1d6u7m6u6h8y2fopx.jpg)

3. Log into your application as administrator. Navigate to single sign-on settings on your application where you set up single sign-on settings
4. Replace the IdP certificate with OPSWAT certificate you downloaded in step 2

![](https://uploads.developerhub.io/prod/97qW/4z0dnowvlbqppam998cvdamqdwl2puzddzs9vp3hv688wlvz3q44i6vlzgcd9jyy.png)

5. Save your changes.
