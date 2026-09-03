<!-- source: https://www.opswat.com/docs/myop/knowledge-base/how-do-i-integrate-entra-id-single-sign-on-with-opswat-central-m -->

# How do I integrate Entra ID Single-Sign On with OPSWAT Central Management?

Integrating **Microsoft Entra ID** Single Sign-On (SSO) with OPSWAT Central Management allows users to authenticate using **Microsoft Entra ID**, improving security and simplifying access control. Here is how to do it:

**Step 1:** Navigate to **Azure Portal** > **Enterprise Applications** and create a **New Application**

**Step 2:** Create your own application > configure a name and click on **Create**

**Step 3:** Once the application is created click on **Set up single sign on**

and select **SAML** sign-on method:

**Step 4:** Scroll down to **3 SAML Certificates**, click on Edit and download the **Base64 Certificate** and **federated certificate XML** and upload them to **OPSWAT Central Management (OCM)** > **Settings > Integrations > Single-Sign On**:

**Step 4.1:** Click on **SAVE** and this will generate the OCM Login/Logout URL:

**Step 5:** On the **Enterprise Application**, go to **Basic SAML Configuration**, click on **Edit** and configure as follows:

**Identifier:** OCM Address

**Reply URL**: OPSWAT Central Management Login URL

**Logout URL**: OPSWAT Central Management Logout URL

**Step 6:** Scroll to **3 SAML Certificates** and once again download the **Base64 Certificate** and **federated certificate XML** and upload them to **OPSWAT Central Management (OCM)** > **Settings > Integrations > Single-Sign On**:

Save the changes and test the SSO Integration from Entra ID side:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
