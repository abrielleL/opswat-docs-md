<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis -->

# How to work with MetaDefender IT Access APIs

This is your reference for taking advantage of MetaDefender IT-OT Access APIs within your environment. Be sure to refer to the [terms and conditions](https://docs.opswat.com/policies/opswat-policies/opswat--inc--terms-of-service) as you develop your applications. Check back often as our APIs are growing to accommodate our user community as well as our platform.

Our APIs allow developers to easily integrate the data available through our MetaDefender IT-OT Access platform into your own applications. This data includes

1. Device details such as device information (Host name, Device ID, MAC/IP Address,...)
2. Device security and compliance status, such as Antivirus, Anti-phishing, Public File Sharing, and Malware detection as well as account information.

These APIs can be used to provide authentication and enforcement via a Secure Access solution (SSL VPN, NAC, etc) or can be integrated into a Remote Monitoring and Management platform for expansive visibility into the endpoints under management. The options are unlimited.

To work with our APIs, you can follow the below steps:

1. Register an OAuth application to achieve a client key and client secret.
2. Implement your application to interact with MetaDefender IT-OT Access APIs

## [Register your application](/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis#register-your-application)

Before getting started, you will need to [set up a MetaDefender IT-OT Access account](/docs/macloud-sdp/configuration---management/get-started) order to begin registering your applications to our platform. Once your account is created, you can proceed with [registering your application.](https://gears.opswat.com/o/app/register) Following submission, applications are confirmed and *Client Key* and *Client Secret* strings are provided. **These keys are unique and should remain confidential**.

Before you register your application through the MetaDefender IT-OT Access oAuth Portal. You will be expected to provide the following information when registering:

- Application name
- Application description - purpose of the application
- Application URL - place where their application resides
- Callback URL - where user is redirected after authorizing application for access to the account

## [Implement your application](/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis#implement-your-application)

MetaDefender IT-OT Access leverages [OAuth 2.0](http://oauth.net/)* technology, so you should be familiar with the OAuth 2.0 specifications and general flow to ensure that your application is capable of supporting the MetaDefender IT-OT Access APIs.

To help you get started with the MetaDefender IT-OT Access APIs, we have developed extensive documentation and sample applications. Click [here](/docs/macloud-sdp/developer-guide/sample-code) read more about how to implement with the APIs or to download the sample code.

*OAuth 2.0 is an open protocol used by OPSWAT for authorization of access to resources within our platform. You can read more about OAuth 2.0 [here](http://oauth.net/2/).

## [Branding Guidelines](/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis#branding-guidelines)

**Application Name**

You will need to provide a name for your application upon registration.

**Company Information**

We will need your application’s logo as part of the application registration process. If you change your company name, application name, logo, or website, please let us know by updating your information in the [MetaDefender IT-OT Access OAuth portal](https://gears.opswat.com/o/app/register).

**OPSWAT Logo and Guidelines**

You are free to use the OPSWAT name and logo in relation to your application, including marketing materials and website content; however, we do ask that you follow the OPSWAT guidelines. If there are any questions, please contact the [OPSWAT Team](https://www.opswat.com/contact).
