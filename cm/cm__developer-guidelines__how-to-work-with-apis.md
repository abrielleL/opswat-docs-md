<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis -->

# How to work with oAuth APIs

This is your reference for taking advantage of My OPSWAT Central Management APIs within your environment. Be sure to refer to[ OPSWAT Terms of Service](https://www.opswat.com/legal/terms-of-service) as you develop your applications. Check back often as our APIs are growing to accommodate our user community as well as our platform.

Our APIs allow developers to easily integrate the data available through our My OPSWAT Central Management platform into your own applications. This data includes

1. Device details such as device information (Host name, Device ID, MAC/IP Address,...)
2. Device security and compliance status, such as Antivirus, Anti-phishing, Public File Sharing, and Malware detection as well as account information.

These APIs can be used to provide authentication and enforcement via a Secure Access solution (SSL VPN, NAC, etc) or can be integrated into a Remote Monitoring and Management platform for expansive visibility into the endpoints under management. The options are unlimited.

To work with our APIs, you can follow the below steps:

1. Register an OAuth application to achieve a client key and client secret.
2. Implement your application to interact with My OPSWAT Central Management APIs

## Register your application

Before getting started, you will need to [set up a My OPSWAT Central Management account](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-saas#set-up-saas-account) in order to begin registering an oAuth applications to our platform. Once your account is created, you can [ registering an oAuth application.](https://www.opswat.com/docs/cm/knowledge-base/how-could-i-retrieve-client-id-and-client-secret-on-my-opswat-ce) to obtain a *Client Key* and *Client Secret* strings for API authentication. **These keys are unique and should remain confidential**.

Before you register your application through the My OPSWAT Central Management oAuth Portal. You will be expected to provide the following information when registering:

- Application name
- Application description - purpose of the application
- Application URL - place where their application resides
- Callback URL - where user is redirected after authorizing application for access to the account

## Implement your application

My OPSWAT Central Management leverages [OAuth 2.0](http://oauth.net/)* technology, so you should be familiar with the OAuth 2.0 specifications and general flow to ensure that your application is capable of supporting the My OPSWAT Central Management APIs.

To help you get started with the My OPSWAT Central Management APIs, we have developed extensive documentation and sample applications. Refer to [Sample Code](https://www.opswat.com/docs/cm/developer-guidelines/sample-code) on how to implement with the APIs or to download the sample code.

*OAuth 2.0 is an open protocol used by OPSWAT for authorization of access to resources within our platform. You can read more about OAuth 2.0 [here](http://oauth.net/2/).

## Branding Guidelines

**OPSWAT Logo and Guidelines**

You are free to use the OPSWAT name and logo in relation to your application, including marketing materials and website content; however, we do ask that you follow the OPSWAT guidelines. If there are any questions, please contact the [OPSWAT Team](https://www.opswat.com/contact).
