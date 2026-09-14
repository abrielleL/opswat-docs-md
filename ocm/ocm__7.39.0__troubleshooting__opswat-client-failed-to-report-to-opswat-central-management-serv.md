<!-- source: https://www.opswat.com/docs/ocm/7.39.0/troubleshooting/opswat-client-failed-to-report-to-opswat-central-management-serv -->

# MetaDefender Endpoint failed to report to OPSWAT Central Management server

| Term | Detail |
| --- | --- |
| Problem | MetaDefender Endpoint failed to report to OPSWAT Central Management server |
| Cause | - OPSWAT Central Management's Server URL has changed. - MetaDefender Endpoint has trouble connecting to an HTTPS-configured OPSWAT Central Management. |
| Troubleshooting | - Go to **Settings > Server Configuration > Device API** and check if the Server URL field is correct. - Check MetaDefender Endpoint's log if there is an issue when connecting to OPSWAT Central Management. |
| Solution | - Update Server URL and reinstall MetaDefender Endpoint on the affected devices. - Correct the connection issue on the system that hosts MetaDefender Endpoint. |

**OPSWAT Central Management's Server URL has changed.**

In the setup wizard, the user has to set the field Server URL, which is the address of the OPSWAT Central Management server that MetaDefender Endpoint will use to connect to. If the OPSWAT Central Management's server changes its address, MetaDefender Endpoint instances still using the old address will be unable to connect.

The solution is to update the Server URL field in **Settings > Server Configuration > Device API** and reinstall MetaDefender Endpoint on the affected devices.

MetaDefender Endpoint **has trouble connecting to an HTTPS-configured OPSWAT Central Management.**

If OPSWAT Central Management has been configured to HTTPS mode, in certain cases, MetaDefender Endpoint will be unable to connect to OPSWAT Central Management due to a certificate error. [Please locate the log of MetaDefender Endpoint to find the exact error](/docs/ocm/7.39.0/knowledgebase/how-do-i-retrieve-the-opswat-client-logs-).

One such error is a missing intermediate certificate, as indicated by the error **CHTTP.Post() failed; error = 60; message = SSL certificate problem: unable to get local issuer certificate** in MetaDefender Endpoint's GEARS-Agent.log.

The users will have to locate the missing intermediate certificate and import it into the system's certificate store on the MetaDefender Endpoint's host system.

The image below shows a Windows system in which the intermediate certificate is imported under **I ntermediate Certification Authorities.** The certificate store can be accessed via **Start Menu > Manage user** certificates.
