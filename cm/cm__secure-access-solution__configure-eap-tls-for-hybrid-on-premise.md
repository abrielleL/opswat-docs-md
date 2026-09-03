<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/configure-eap-tls-for-hybrid-on-premise -->

# Configure EAP-TLS for On-premise

## Introduction

This document describes how to set up Windows Group Policy to allow domain machines to automatically perform 802.1x EAP-TLS authentication against RADIUS NAC.

## Configuration EAP-TLS for NAC Edge

### Install Active Directory Certificate Services

```powershell
# Check if the Active Directory Certificate Service is installed
Get-WindowsFeature AD-Certificate

# To install the Certification Authority features, run the following cmdlet:
Install-WindowsFeature ADCS-Cert-Authority -IncludeManagementTools

# Configuring the Active Directory Certificate Services with Enterprise CA
Install-ADcsCertificationAuthority -CAType EnterpriseRootCa
```

We use PowerShell for install and config ADCS. (Make sure the run the following commands as Administrator from a Domain Controller in your domain)

### Export Certificate from CA and Import to NAC

#### Export Certificate from CA

Go to Start > Run. Enter `cmd`, press Enter, then enter the command below at the prompt:

```plaintext
certutil -ca.cert ca_name.cer
certutil -encode ca_name.cer ca_name.pem
```

#### Import Certificate to NAC Edge

Login to your **My OPSWAT Central Management** console

From **RADIUS NAC** → **Configuration** → Click on **Edge** Type → **Authentication Methods**→ **EAP-TLS.**

![](https://uploads.developerhub.io/prod/97qW/czvs0zcmifefv7kds98duxmkd8mpa5tv3l2iik2u85ix8ntymn7paf7rbg07nlzj.png)

Select the exported **.pem** file.

![](https://uploads.developerhub.io/prod/97qW/4v4y9st8ncr22tun445yy3njmb1zs3i12ok5voc7ppyvaltc8584f1ckoo2cp26y.png)

Save change

![](https://uploads.developerhub.io/prod/97qW/72x1iapr8261k630xk6i5k6318vq4h55rodyhdzblekwmi1sbxx33tm235e4xsjj.png)

#### Apply the configuration

Click on the **Apply** button to publish changes

![](https://uploads.developerhub.io/prod/97qW/sy4wqt1ou9gj19d33k49mu2ayl7pqdq5909ks11h3xf8vnwlfimtqs806iq6bjx2.png)

## Common configuration for EAP-TLS

#### Auto Enroll Certificates with Group Policy

#### Prepare Certificate Template For Computer and User

1. Open **Certification Authority** tool.
2. Right click on **Certificate Templates** and then click **Manage**.
3. Right-click the **Computer** template, select **Duplicate Template** and specify the following:
   - Under **Compatibility Settings**, specify Certification Authority=**Windows Server 2003** and Certificate recipient=**Windows XP/Server 2003**.
   - Click the **General** tab, and change the Template display name to **Computer_Auto_Enrollment**.
   - Click the **Security** tab, and give "Domain Computers" permissions to **Read,** **Enroll** and **Autoenroll**.
   - Additionally, give 'Domain Controllers' permissions to **Read**, **Enroll** and **Autoenroll**. This is required as the DC computer account will request the policy server for validation rather than the logged-in user.
   - Select the **Subject Name** tab, and change the Subject name format to **DNS Name**.
   - Select **DNS Name** in the subject alternative name.
   - Under the **Request Handling** tab, clear **Allow private key to be exported.** If the requirement is to be able to export private key, leave this checked.
   - Click **OK** to go back to the template list.
4. Right-click the **User** template and select **Duplicate Template** and specify the following:
   - Under **Compatibility Settings**, specify Certification Authority**=Windows Server 2003** and Certificate recipient=**Windows XP/Server 2003**.
   - Click the **General** tab, and change the Template display name to **User_Auto_Enrollment**. If the requirement is to Publish the User certificate in Active Directory and Credential Roaming is enabled, ensure to select both **Publish certificate in Active Directory** and **Do not automatically re-enroll if a duplicate certificate exists in Active Directory**.
   - Select the **Security** tab, and give "Domain Users" permissions to **Enroll** and **Autoenroll**.
   - Select the **Subject Name** tab, and change the Subject name format to **Common name**.
   - Clear **Include email name in subject name** and clear **Email name** in the subject alternative name.
   - Select **User principal name (UPN)**.
   - Under the **Request Handling** tab, clear **Allow private key to be exported**. If the requirement is to be able to export private key, leave this checked.
   - Click **OK** to go back to the template list and then close the **Certificate Templates Console** window.

#### Issue Certificate Template

Right click on **Certificate Template-New-Certificate Template to Issue**, and select both **Computer_Auto_Enrollment** & **User_Auto_Enrollment**

![](https://uploads.developerhub.io/prod/97qW/cicr2jf7a68app1t2p9xooq62kno0qci0oq9pg9m4pl44ehlfiwixpjj6deb8y8e.png)

#### Configuration Of Group Policy

Set the **Configuration Model = Enabled** in **Computer Configuration – Windows Settings – Security Settings – Public Key Policies – Certificate Services Client – Auto Enrollment** in **Default Domain Policy** to enable Certificate Auto Enroll for all domain computers

![](https://uploads.developerhub.io/prod/97qW/1gn1ajnrlww73awj2zw9xboiwgltaj2oixexa0nh6kqkk845kkvb6jfwef5cu0qh.png)

Set the **Configuration Model = Enabled** in **User Configuration – Windows Settings – Security Settings – Public Key Policies – Certificate Services Client – Auto Enrollment** in **Default Domain Policy** to enable Certificate Auto Enroll for all domain users

![](https://uploads.developerhub.io/prod/97qW/6rrqy8o8f13qjw9lltk7gskiagk34mxov0mgzl3a34sfn0gwp7xl436b9aw8x0wp.png)

#### Auto Enroll Certificates With Group Policy For Windows 10

Computer & User Certificate will be generated automatically when Group Policy is updated in the background every 90 Minutes

```powershell
#can be used to force latest GPO to be applied on users’ workstation immediately
gpupdate _force
```

#### Deploy Group Policy for Wireless and Wired Networks

#### Group Policy for EAP-TLS authentication to a Wireless Network

- Under **Computer Configuration – Windows Settings – Security Settings – Wireless Network (IEEE 802.11) Policies**
- Enter **Policy Name**, **Description** and click **Add** – **Infrastructure**
- Enter the **SSID** **Name** and click **Add**
- Select the following
  - Authentication = **WPA2-Enterprise**
  - Encryption = **AES-CCMP**
  - Network Authentication Method = **Microsoft: Smart Card or Other Certificate**
  - Authentication Mode = **User or Computer Authentication**

![](https://uploads.developerhub.io/prod/97qW/ic9nn12wphcs9fpjqfesky5953bsrm245g5ed7h4zc5tkvqbtp8dvir7ch2czus9.png)

NOTE: If you are using a self-signed RADIUS certificate instead of the default "portal.myweblogon.com" certificate, you should click the "Properties..." button next to the "Select a network authentication method" drop-down on the right-most screen, and choose your self-signed certificate from the list in the window that appears.

#### Group Policy for EAP-TLS authentication to a Wired Network

Please follow the same steps as on previous part, but select "**Wired Network (IEEE 802.3) Policies**" under "**Security Settings**".

![](https://uploads.developerhub.io/prod/97qW/f26kjkutova91m7ovunllfqgvkaznyd3vr5eqkjzw0um7me6ijq2nbqxio7234b2.png)

### Computer is connected to WIFI automatically when GPO applied

By default, when User open **certmgr**, a certificate should be available

![](https://uploads.developerhub.io/prod/97qW/rqjvx124fxwixrd9otu8276kmo0a6ydwkpnqv1jdbyx9a0xx52jmtnlspdn0piwh.png)

As long as the certificate still available, user will connect to WIFI successfully

![](https://uploads.developerhub.io/prod/97qW/27hpove1tjyq0emm2z03z9f78lii2pwcj0tnqnjorbclnlfofgetm3ge5p24e4ci.png)
