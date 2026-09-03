<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/okta-identity-engine---authentication-policies-advance-mode-with -->

# Okta Identity Engine - Authentication policies Advance Mode with Policy API

## Setup Steps

After Okta IdP MFA is setup for My OPSWAT Central Management, follow these steps to configure Authentication policies for Okta Dashboard with My OPSWAT Central Management IdP MFA as the only possession MFA factor.

1. Create an Okta API token.

Reference: [https://help.okta.com/oie/en-us/content/topics/security/api.htm#create-okta-api-token](https://help.okta.com/oie/en-us/content/topics/security/api.htm#create-okta-api-token)

![](https://uploads.developerhub.io/prod/97qW/njit4q3mui8vo1uy7p9qwmiw46njrynyd2r1gacknak9dyclt1pganva9pdt7pow.png)

2. Explore the Okta Policy API with Postman.

Reference: [https://developer.okta.com/docs/reference/api/policy/#get-started](https://developer.okta.com/docs/reference/api/policy/#get-started)

In Postman, go to Environments and input variables

![](https://uploads.developerhub.io/prod/97qW/htaaigfsu7nywrzhiky6uzewem1vvfr8szl8peuyfd2o55mxjt0irk0a45g20331.png)

- baseUrl: your Okta domain https endpoint
- apikey: the API token created from Step 1.

3. Make an API call "[PUT] Replace a Policy Rule".

![](https://uploads.developerhub.io/prod/97qW/j421c6eg8atulh658i15q250sd6jma0cvoklvahhebt9i2g4wc4boxnxdcz0ae5d.png)

- Input **policyId** and **ruleId**
- Update the rule with expecting *"verificationMethod"*, *"factorMode"* and *"constraints"*

Reference: [https://developer.okta.com/docs/reference/api/policy/#verification-method-object](https://developer.okta.com/docs/reference/api/policy/#verification-method-object)

**Note:** the configured My OPSWAT Central Management IdP MFA has authenticator method as **IDP**

![](https://uploads.developerhub.io/prod/97qW/l239oy2m30fic788e6cvlveap44b8xypsmw1bua7jy5jvtgch5wwk2isl4fyblu6.png)

![](https://uploads.developerhub.io/prod/97qW/ob5grgtroeh7jn9zca4bpi4vnppxwi27xfqtpzohjbttcehyi5xek5p8dshucgv3.png)

Reference: [https://developer.okta.com/docs/reference/api/policy/#authenticator-key-type-method-and-characteristic-relationships-for-constraints](https://developer.okta.com/docs/reference/api/policy/#authenticator-key-type-method-and-characteristic-relationships-for-constraints)

- Click Send

![](https://uploads.developerhub.io/prod/97qW/rq6ga2y2zwarvzg3b3xulsruf87c0icpb4cyt0g0146zayd1hj0zbimgnl4vr9t4.png)

4. Verify your Policy API configuration.

In Okta, go to **Security** > **Authentication Policies** > go to configured policy and rule

![](https://uploads.developerhub.io/prod/97qW/c2du9od5ljcxzqkyxgv1zwl6sanhex68kxutmkfgjf9vhwgi8rj3x5y5ytptxryd.png)

The rule updated by Policy API should appear in Advance mode (JSON).
