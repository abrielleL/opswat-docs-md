<!-- source: https://www.opswat.com/docs/cm/integrations/known-issues -->

# Known Issues

The MetaDefender IT Access API Input doesn’t support any inputs that requires multiple API calls in sequence, for ex: [Get Threats API](https://www.opswat.com/docs/cm/developer-guide/get-threats) needs a device id body parameter however Add-on is not designed to get all Device IDs associated with an account first and then pass then one by one to Get Threats API call.
