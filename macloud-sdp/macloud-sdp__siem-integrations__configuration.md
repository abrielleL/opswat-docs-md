<!-- source: https://www.opswat.com/docs/macloud-sdp/siem-integrations/configuration -->

# Configuration

This section guides you how to configure the add-on to collect data from your MetaDefender IT-OT Access accounts.

## [Pre-requisites](/docs/macloud-sdp/siem-integrations/configuration#pre-requisites)

- Register an OAuth application through your OPSWAT account via [MetaDefender IT-OT Access OAuth Portal](https://console.metaaccess-b.opswat.com/o) and get an client key and client secret that is needed to configure an account for the add-on. Please find detailed steps [here](/docs/macloud-sdp/kb/how-could-i-retrieve-client-id-and-client-secret-on-metaaccess-t).
- Implement the required firewall rules to enable your Splunk Forwarder to make API calls to port 443 of your OPSWAT on-prem/cloud server.
- Create an index (for example: opswat) that will be used to store the data retrieved by this add-on.
