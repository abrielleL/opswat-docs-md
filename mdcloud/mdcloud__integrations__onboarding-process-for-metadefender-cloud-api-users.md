<!-- source: https://www.opswat.com/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users -->

# Onboarding Process for MetaDefender Cloud API Users

## [Create a New OPSWAT Account](/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users#create-a-new-opswat-account)

- Go to the registration page: <https://id.opswat.com/register>
- Fill in the form
- Submit the form, and you will receive a confirmation email
- Confirm activation by clicking the link in the confirmation email
- Note that an OPSWAT account grants you free access to other OPSWAT products, such as:

  - [MetaDefender Cloud](https://metadefender.opswat.com)
  - [MetaAccess](https://www.opswat.com/free-tools/free-endpoint-security-scan)
  - [OPSWAT Portal](https://portal.opswat.com/)
  - [OPSWAT Support](https://www.opswat.com/support)

## [Obtain Your API Key](/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users#obtain-your-api-key)

- Go to <https://metadefender.opswat.com/> and log in with your new account credentials
- After logging in, go to your [Account Information page](https://metadefender.opswat.com/account)
- The section "API Key Information and Limits" displays your API key

If you have purchased a standard, professional, or enterprise license of MetaDefender Cloud, the flag "Paid user" will be set to "Yes," and you will see your expiration date and purchased usage limits.

## [Test Your API Key with Our APIs](/docs/mdcloud/integrations/onboarding-process-for-metadefender-cloud-api-users#test-your-api-key-with-our-apis)

- MetaDefender Cloud offers a rich set of publicly available APIs – [see our documentation for the complete list](https://onlinehelp.opswat.com/mdcloud/5._Endpoints.html)
- View the hash lookup API, and copy your API key from your account to the example curl commands listed on the right
- If you encounter any problems during this process, you can contact OPSWAT via: [OPSWAT Support](https://www.opswat.com/support) or see our [Community Forum](https://go.opswat.com/OPSWATCommunity/s/)
- Every response from MetaDefender Cloud APIs exposes Rate Limiting headers informing what your current usage is and when it will be reset. Read more about [rate limiting](/docs/mdcloud/integrations/rate-limiting)

# Single Hash Lookup
$ curl -vvvv https://api.metadefender.com/v4/hash/66DA1A91E1ED5D59BECFAD85F53C05F9 -H "apikey: $YOUR_API_KEY"
