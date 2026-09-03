<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/microsoft-entra-id-with-aws-workspaces -->

# Microsoft Entra ID with AWS WorkSpaces

My OPSWAT Central Management can be easily integrated with an Microsoft Entra ID & AWS WorkSpaces integration to ensure that a device is compliant with the organization's security policy before it is granted access to AWS WorkSpaces. This ensures that the user is not only authenticated by Microsoft Entra ID, but also a device the user uses to access SaaS applications tested for risks and vulnerabilities such as infections or outdated operating systems, BEFORE it accesses an organization's cloud services.

Follow below steps to integrate My OPSWAT Central Management with your Microsoft Entra ID & AWS WorkSpaces.

## Step 1. Complete the prerequisites

Complete the following prerequisites before integrating with My OPSWAT Central Management:

- Create a WorkSpace. For more information, see the AWS WorkSpaces documentation: [https://docs.aws.amazon.com/workspaces/](https://docs.aws.amazon.com/workspaces/)
- Configure your Microsoft Entra ID IdP to establish a SAML‑based trust relationship with AWS WorkSpaces. For detailed configuration steps, refer to the Amazon WorkSpaces SAML Authentication Implementation Guide: [https://d1.awsstatic.com/workspace-saml-guide.pdf](https://d1.awsstatic.com/workspace-saml-guide.pdf)

## Step 2. Get Information From Microsoft Entra ID Saml Application

1. Log in to the Microsoft Entra console.
2. Navigate to **Enterprise Application** > **Your Application**
3. Navigate to the **Properties tab** and copy the **User access URL**

![](https://uploads.developerhub.io/prod/97qW/z89pqk6zbh0x1c19kci0vhhs6ft58m445ypyuuxrjs3y6sb86v7vv57qcgqnau70.png)

4. Navigate to the Single Sign-on tab, copy the Reply URL

![](https://uploads.developerhub.io/prod/97qW/1e35v3uoq7irwzt0789vr2ckpj35j8vxsljwk51kgvex5z1dbf35gx90dm18e0gd.png)

5. Copy **Login URL**

![](https://uploads.developerhub.io/prod/97qW/ibrmrgecvcrwi8jskm589r7autsx732mlri6np4jrql6osvoizafjm6te6taysog.png)

## Step 3. Add application and configure Access Rules on My OPSWAT Central Management

1. Log in to the My OPSWAT Central Management console.
2. Navigate to **Secure Access** > **Protected Apps**
3. Check **"Enable Secure Access".**
4. Click **SAVE**.
5. Click **Add Protected Application** then choose **IDP METHOD** option
6. Choose option **Add new IDP**, enter the name, and upload the certificate got in step 2.3. Then click **Continue**

![](https://uploads.developerhub.io/prod/97qW/iyb687fe8vpkeeoepu9sr5r4bfziisseuez3akqctg9ejvvd44fvlglkmy52p1by.png)

5. Enter the required fields
   1. *Application:* application name, for example: AWS Workspaces
   2. *IdP Login URL*: fill in the link that you have from Step 2.3 (User Access URL)
   3. *IdP Start URL*: fill with the link that you have from Step 2.5 (Login URL)
   4. *App ACS URL*: fill with the link that you have from Step 2.4 (Reply URL / ACS URL)
   5. *Access Mode:* pick an access mode you prefer. See details on the access modes at [Step 2. Add protected applications with IdP Method](https://onlinehelp.opswat.com/metaaccess/Step_2._Add_protected_applications_with_IdP_Method.html)

![](https://uploads.developerhub.io/prod/97qW/gccrq8cugjninerwwans5hkyrphpwap4ldvkslt7u3x6r2ygg9opz58nazu87z0g.png)

6. After saving successfully, a SSO setup instruction will be shown, copy the ACS URL My OPSWAT Central Management generated there and download the OPSWAT Certificate. Note that this information can be found in the protected app's details later.

![](https://uploads.developerhub.io/prod/97qW/4gi7qr2b3o1oy5i6anwnxlvnvzgjo7bqpy2fecczkb3nyddei3utld95wdjltrw4.png)

## Step 4. Update Applications settings on Entra ID

1. Log into Entra Portal as Administrator, then go to your application
2. Navigate to your application
3. Select Single sign-on
4. Click the edit icon (pencil icon) on Basic SAML Configuration section
5. Replace **Reply URL** with the My OPSWAT Central Management URL which you got from Step 3.6

![](https://uploads.developerhub.io/prod/97qW/p5n7tj3p5stsmdrqlxqd65lioo5ijexi6kuzd4orbljlfywtqdq07fxy2i75u0ih.png)

6. Click **Save. Note:** It may take some time for Entra ID to apply your changes.

## Step 5. Configure SSO setting on AWS Identity Providers

1. Open the certificate from Step 3.6 with notepad, remove all the break lines, then copy the content only. For example:

```plaintext
MIIDhDCCAmygAwIBAgIGAZO2xuJ7MA0GCSqGSIb3DQEBCwUAMIGCMS0wKwYDVQQDDCRjOTU5MDFlNi0xZTczLTQ3ZDMtOGE4YS03NzRmMDk5ZTQ5NzYxFDASBgNVBAsMC09wc3dhdCwgSW5jMRQwEgYDVQQKDAtPcHN3YXQsIEluYzELMAkGA1UEBwwCU0YxCzAJBgNVBAgMAkNBMQswCQYDVQQGEwJVUzAeFw0yNDEyMTExNzMxNDdaFw0zNDEyMTExNzMxNDdaMIGCMS0wKwYDVQQDDCRjOTU5MDFlNi0xZTczLTQ3ZDMtOGE4YS03NzRmMDk5ZTQ5NzYxFDASBgNVBAsMC09wc3dhdCwgSW5jMRQwEgYDVQQKDAtPcHN3YXQsIEluYzELMAkGA1UEBwwCU0YxCzAJBgNVBAgMAkNBMQswCQYDVQQGEwJVUzCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBANzFODN8VEvezs0K3NPaa33zd8rkIbP1SfI010HF9qEGsCZyxtDhiGKojMOkUspsNbuy1Je4aWVO8FFcXrp+Wf8bu1vRHi1gHUYn/Zhp1ktVJS/hEYxE4fs7UW770MYH2MN5GrUgqi3THOaG0UPg/8pkXxkjY6wc03EXMxdZUAT1t6wiIFTL+0OlwqoNLBPgVzSaVLmXawlrg+BDU5um/H8QcMyJVVTl1o+/VDwXKGpvK+1b8+8XyvDILogF8yM33uvcpqNxWr7bGOySJdQjwX+5tp2AUMpxL8avEpLu4p2WWV6K15vfBWdMSZExhmY6nJGX4z5FF/Fu27pLFBAPXLECAwEAATANBgkqhkiG9w0BAQsFAAOCAQEAK3oGjiuloDP5fo3/2XPf3g53cXpuRhMqg4jbxEtOsXsQ2byQKohNMnje3uPKJvAGiBFTDjt6DF2dEQ+pltZhwWMiGwUcAmTIEQRRczO+Doulbm/dOrSxhHdE7jiU54Zm0A4Nu+JV0GiHWGYsRTHzqXDuw/gfx3TU+OWkCwlQ2zs/D36pbV5C8Pqdk6VYDIyyXbT1ngX+1p+bVGsW9NRSArv92qUOSoCcifMa7HHmFRS5rEuXDFaJ+KPWS4V24vN7aoSd2kBaPfu7kP/LSDfo1awdUCJ+IPFAVWaPWzfPAj24iYy/HYcfwpHY0w1REoJcKqtbkzIBjy2uD2oAoUgJbA==
```

2. Login to your Aws Account. Navigate to **IAM** > **Identity providers**, then choose your Identity provider.
3. Download the metadata

![](https://uploads.developerhub.io/prod/97qW/tyjd3kwrs80z93wibwo0ukh1hiyh3w59tt2d23rc0lr9y8j0ey75z94nlhy97gyn.png)

4. Open the metadata file using Notepad and update every certificate value (in the `<ds:X509Certificate>` and `<X509Certificate>` tags) with the one provided in step 5.1. You must update all certificate entries; otherwise, you will receive the error: "No valid roles associated with the account."
5. Replace metadata with the updated file

![](https://uploads.developerhub.io/prod/97qW/3i2yenzpry8cs3mwin175sgxpi3reubivfj66t1tfzbpjs4cvyhgdq72txk2nbar.png)

**DONE! CONGRATULATIONS.** Log in as normal to test your integration and verify if it works as expected.
