<!-- source: https://www.opswat.com/docs/cm/developer-guidelines/overview -->

# Overview

This document walks you through steps to integrate My OPSWAT Central Management to your existing solutions to enforce device posture check.

A few integration use cases include:

- empower your existing SSL VPN/NAC solution with My OPSWAT Central Management by checking device security prior to access to your network
- Include My OPSWAT Central Management as a feed into your RMM (Remote Monitoring & Management) platform for full visibility into the security and compliance state of your environment.
- Integrate My OPSWAT Central Management into your existing MDM solution to assess the security and compliance state on new BYOD devices

## How does it work?

![](https://uploads.developerhub.io/prod/97qW/o041eo12mmgsztyivs700frb8uvnpzu5hx76is57573jrj1d7kv3fl75ycsu2m4g.png)

My OPSWAT Central Management agent runs on an endpoint and periodically checks compliance status of the device against a security baseline (policy) configured on your My OPSWAT Central Management account. This compliance information for the endpoint is stored locally and also available from the My OPSWAT Central Management cloud. Your solution uses the compliance information to make enforcement actions.

When a user accesses to your service, your solution needs to query My OPSWAT Central Management via [our oAuth APIs](https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis) or use [compliant status stored on a device](https://www.opswat.com/docs/cm/developer-guidelines/custom-policy-check) to check the device's compliant status. After getting device status, your solution then makes decision on granting access for the device and shows error messages to end-user in each use case.

You can use either device MAC address or device ID to query device health and compliance status via oAuth APIs. My OPSWAT Central Management generates an unique identity for each device and offers multiple mechanisms to retrieve Device ID such as [browser cookies](https://www.opswat.com/docs/cm/developer-guidelines/browser-cookies), [client certificates](https://www.opswat.com/docs/cm/developer-guidelines/client-certificates), and [cross-domain API](https://www.opswat.com/docs/cm/developer-guidelines/cross-domain-api).

**A comparison of solutions to retrieve Device ID**

|  | Registry or p-list values | Browser Cookie | Agent Certificate | Cross-domain API | Universal Link |
| ---- | ---- | ---- | ---- | ---- | ---- |
| Agent required | Yes | No | No | No | No |
| User right | admin | All | All | All | All |
| OS | Windows and macOS | Windows only | Windows and macOS | Windows, macOS, and Linux | Android and iOS |
| Reliability | High | Low | High | High | High |
| Browsers | All | IE, Firefox, Chrome | IE, Firefox, Chrome, Safari | All | All |
| Browser mode | All | Not support Incognito or In Private mode | All | All | All |
| User Interaction | No | No | Maybe | No | Yes |
| Security | High | Low | High | High | High |
| Can be deleted accidentally by user | No | Yes | No | No | No |

## How could I integrate my solution with My OPSWAT Central Management?

It's easy to integrate with the My OPSWAT Central Management platform, and the available APIs allow you to efficiently integrate the My OPSWAT Central Management features with your own solution. From the agent to the cloud, we have you covered.

![](https://uploads.developerhub.io/prod/97qW/z9s0zdc0potwnia2bz8fvbc5szu6tqp67leoz1glg2u7un8g7m7zp8djxga5ru2y.png)

## Sign Up For An Account

You will need to [set up](https://www.opswat.com/docs/cm/onboarding-guide/onboarding-guide-saas#set-up-saas-account) a My OPSWAT Central Management account in order to begin your work. Once your account is created, you can proceed to log into My OPSWAT Central Management console to set up your My OPSWAT Central Management account[.](https://gears.opswat.com/developers/app/register) You may monitor up to 50 devices for your development free of charge. If you would like to add more devices to your account, please [contact our Sales](https://www.opswat.com/contact) for pricing information.

## Read Our Documents

Before you begin your implementation, you will need to identify your specific use case:

- API based application: If you wish to create an application to fetch data (devices, device compliance status, reports,...) or do batch actions (delete devices, exempt devices, ...) on your account, you check [this documentation](https://www.opswat.com/docs/cm/developer-guidelines/how-to-work-with-apis).
- Integration: If you wish to integrate My OPSWAT Central Management with your solution, [this document](https://www.opswat.com/docs/cm/developer-guidelines/overview) is here for your reference.
- If you would like to prevent risky devices from accessing your resources, you can check out [our secure access solutions](https://www.opswat.com/docs/cm/secure-access-solution/overview).

## Start Implementation

You may now start implementing/configuring your applications/solutions. Be sure to refer to this user guide for detailed information on any issues you might wish to troubleshoot.

## Test Your Solution

It's time for you to test your work. Before testing, you need to back to your My OPSWAT Central Management console to download a proper agent and install it on your endpoints. Read our KB [How do I deploy or distribute MetaDefender Endpoint to my devices?](https://www.opswat.com/docs/cm/knowledge-base/how-do-i-deploy-or-distribute-metadefender-endpoint-to-my-device) to know how to distribute MetaDefender Endpoint to your devices.

## Release

Congratulations! You got there. You can celebrate a party to say cheers with your team.

If you would like to enhance device security check on your existing solution, check out our existing integrations [NAC or SSL VPN](https://www.opswat.com/docs/cm/secure-access-solution/nac-or-ssl-vpn).
