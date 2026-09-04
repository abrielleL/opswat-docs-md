<!-- source: https://www.opswat.com/docs/macloud-sdp/developer-guide/integration-guidelines -->

# Integration guidelines

This document gives you a guideline how to integrate MetaDefender IT Access to your existing solution to enforce device posture check.

A few integration use cases include:

- empower your existing SSL VPN/NAC solution with MetaDefender IT Access by checking device security prior to access to your network
- Include MetaDefender IT Access as a feed into your RMM (Remote Monitoring & Management) platform for full visibility into the security and compliance state of your environment.
- Integrate MetaDefender IT Access into your existing MDM solution to assess the security and compliance state on new BYOD devices

## [How does it work?](/docs/macloud-sdp/developer-guide/integration-guidelines#how-does-it-work)

MetaDefender IT Access agent runs on an endpoint and periodically checks compliance status of the device against a security baseline (policy) configured on your MetaDefender IT Access account. This compliance information for the endpoint is stored locally and also available from the MetaDefender IT Access cloud. Your solution uses the compliance information to make enforcement actions.

When a user accesses to your service, your solution needs to query MetaDefender IT Access via [our OAuth API](/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis) use [Custom Policy Check](/docs/macloud-sdp/developer-guide/custom-policy-check) to check the device's compliant status. After getting device status, your solution then makes decision on granting access for the device and shows error messages to end-user in each use case.

You can use either device MAC address or device ID to query device health and compliance status via OAuth API. MetaDefender IT Access generates an unique identity for each device and offers multiple mechanisms to retrieve Device ID such as [Browser Cookies](/docs/macloud-sdp/developer-guide/browser-cookies), [Agent Certificate](/docs/macloud-sdp/developer-guide/client-certificate) and [Cross-Domain API](/docs/macloud-sdp/developer-guide/cross-domain-api) endpoints are running persistent agents

**A comparison of solutions to retrieve Device ID**

|  | Registry or p-list values | Browser Cookie | Agent Certificate | Cross-domain API | Universal Link |
| --- | --- | --- | --- | --- | --- |
| Agent required | Yes | No | No | No | No |
| User right | admin | All | All | All | All |
| OS | Windows and macOS | Windows only | Windows and macOS | Windows, macOS, and Linux | Android and iOS |
| Reliability | High | Low | High | High | High |
| Browsers | All | IE, Firefox, Chrome | IE, Firefox, Chrome, Safari | All | All |
| Browser mode | All | Not support Incognito or In Private mode | All | All | All |
| User Interaction | No | No | Maybe | No | Yes |
| Security | High | Low | High | High | High |
| Can be deleted accidentally by user | No | Yes | No | No | No |

## [How could I integrate my solution with MetaDefender IT Access?](/docs/macloud-sdp/developer-guide/integration-guidelines#how-could-i-integrate-my-solution-with-metadefender-it-access)

It's easy to integrate with the MetaDefender IT Access platform, and the available APIs allow you to efficiently integrate the MetaDefender IT Access features with your own solution. From the agent to the cloud, we have you covered.

## [Sign Up For An Account](/docs/macloud-sdp/developer-guide/integration-guidelines#sign-up-for-an-account)

You will need to set up a MetaDefender IT Access account in order to begin your work. Go [here](https://go.opswat.com/communityRegistration?app=0sp1a000000GmuY) to create an account on OPSWAT Portal. Once your account is created, you can proceed to log intoMetaDefender IT Access [console](https://gears.opswat.com) to set up your MetaDefender IT Access account[.](https://gears.opswat.com/developers/app/register) You may monitor up to 50 devices for your development free of charge. If you would like to add more devices to your account, please [contact our Sales](https://www.opswat.com/contact) for pricing information.

## [Read Our Documents](/docs/macloud-sdp/developer-guide/integration-guidelines#read-our-documents)

Before you begin your implementation, you will need to identify your specific use case:

- API based application: If you wish to create an application to fetch data (devices, device compliance status, reports,...) or do batch actions (delete devices, exempt devices, ...) on your account, you should go through our [MetaDefender IT-OT Access APIs](/docs/macloud-sdp/developer-guide/how-to-work-with-metaaccess-apis) documents.
- Integration: If you wish to integrate MetaDefender IT Access with your solution, [146626850](https://onlinehelp.opswat.com/metaaccess/4._Integrations.html#src-5719769) document is here for your reference.
- If you would like to prevent risky devices from accessing your cloud applications through SAML SSO, you can check out how to configure your IdP and applications [here](https://onlinehelp.opswat.com/metaaccess/3.1._SAML_IdP_Method.html)

## [Start Implementation](/docs/macloud-sdp/developer-guide/integration-guidelines#start-implementation)

You may now start implementing/configuring your applications/solutions. Be sure to refer to this user guide for detailed information on any issues you might wish to troubleshoot.

## [Test Your Solution](/docs/macloud-sdp/developer-guide/integration-guidelines#test-your-solution)

It's time for you to test your work. Before testing, you need to back to your [MetaDefender IT Access console](https://gears.opswat.com) to download a proper agent and install it on your endpoints. Read our KB [How do I deploy or distribute MetaDefender Endpoint to my devices?](/docs/macloud-sdp/kb/how-do-i-deploy-or-distribute-opswat-client-to-my-devices-)? to know how to distribute MetaDefender Endpoint to your devices.

## [Release](/docs/macloud-sdp/developer-guide/integration-guidelines#release)

Congratulations! You got there. You can celebrate a party to say cheers with your team.

If you would like to enhance device security check on your existing solution, check out our existing integrations [here](/docs/macloud-sdp/integrations/nac-or-ssl-vpn).
