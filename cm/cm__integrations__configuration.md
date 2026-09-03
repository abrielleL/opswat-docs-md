<!-- source: https://www.opswat.com/docs/cm/integrations/configuration -->

# Configuration

This section guides you how to configure the add-on to collect data from your MetaDefender IT Access accounts.

## Pre-requisites

- Register an OAuth application through your OPSWAT account on [My OPSWAT Central Management console](https://my.opswat.com/portal/central-management) and get an client key and client secret that is needed to configure an account for the add-on. Please find detailed steps [here](https://www.opswat.com/docs/cm/knowledge-base/how-could-i-retrieve-client-id-and-client-secret-on-my-opswat-ce).
- Implement the required firewall rules to enable your Splunk Forwarder to make API calls to port 443 of your OPSWAT on-prem/cloud server.
- Create an index (for example: opswat) that will be used to store the data retrieved by this add-on.
