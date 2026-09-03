<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/radius-logs-for-troubleshooting -->

# RADIUS Logs for Troubleshooting

Choose the “View Logs” option from the left hand navigation. The logs interface provides visibility into each of the RADIUS logs on the appliance as well as the ability to export logs. Each of the logs contain different information as follows:

- **RADIUS Server Log:** Includes high level RADIUS server information.
- **Accounting Log:** Includes the full details contained in RADIUS accounting.
- **Reply Log:** Includes the response messages sent to the wireless controller or AP as the result of an Access-Request. This log will display Access-Accepts and Access-Reject messages.
- **COA Log:** Includes information on any Change of Authorization or Disconnect requests NAC sends to the wireless controller or AP.
- **Service Log:** Includes a low level log of NAC's interaction with the RADIUS services as well as information on joining and leaving the Active Directory Domain.

To export a RADIUS log file, choose the “Archives” tab and then select the log and data range you would like to export. Once your selection is made, click on the “Create Archive” button.

After creating and archive, it will appear in the list as an option to download.
