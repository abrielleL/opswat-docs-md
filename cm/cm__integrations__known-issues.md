<!-- source: https://www.opswat.com/docs/cm/integrations/known-issues -->

# Known Issues

My OPSWAT Central Management API Input doesn’t support any inputs that requires multiple API calls in sequence, for example [Get Threats](https://www.opswat.com/docs/cm/developer-guidelines/get-threats) API needs a device id body parameter however Add-on is not designed to get all Device IDs associated with an account first and then pass then one by one to Get Threats API call.
