<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/how-it-works-idpmfa -->

# How It Works

## How it works

IdP MFA is a device compliance access control solution that leverages the Multi-Factor Authentication flow in Service Provided applications. Communication with your Service Provider is done with SAML, which returns a successful response for compliant devices that have the MetaDefender Endpoint installed.

The Endpoint Client Device is in constant communication with My OPSWAT Central Management, sending device information to help determine its compliance status.

![](https://uploads.developerhub.io/prod/97qW/n7gu7jw979xage79qyei8dqkhjybgk5z09flss4v1jxlh3e2v3ofxqg6wpl590wd.png)

Users attempt to initiate a login from their Service Provider’s dashboard, or launch an application managed by their Service Provider.

1. The Service Provider will send a Multi-Factor verification request to My OPSWAT Central Management
2. My OPSWAT Central Management will determine if the device is either compliant or not compliant
   1. If compliant, the user will return to the Service Provider with a successful authentication
   2. If not compliant, the user will be redirected to a remediation page specifying details on exactly why their device is not compliant.
3. After a successful authentication, the user will be able to navigate to their Service Provider’s dashboard and access their applications.
