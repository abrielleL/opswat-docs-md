<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan -->

# Self Scan

Self-scan feature in Kiosk 4.7.6 is not functioning as expected with Core 5.14.2. When a Self-scan is initiated, all files are skipped and not scanned.

MetaDefender Kiosk has the ability to do a full scan of the system drive to search for threats and shut down Kiosk if necessary. The Kiosk UI must be up and running for this feature to work. It is recommended that in a networked environment that you remotely access the Kiosk's web management console to initiate the on-demand self scanning feature. Configuration options for this feature are found in the Logs section. You can choose to scan the system now or schedule scans to reoccur at the time of your choosing after a configurable number of days or on certain weekdays.

To use the Self Scan feature, navigate to Workflows > enable Self Scan Workflow. Click on Edit button to start configuring the setting for Self Scan

## [Self Scan Configurations](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#self-scan-configurations)

Starting with Kiosk 4.7.5, the Self Scan feature has its own dedicated workflow. Administrators can configure specific settings and define Core workflows for Self Scan. To adjust these settings, go to Self Scan Workflow > Processing

Refer to the following KB ([link](https://www.opswat.com/docs/mdkiosk/operating/selecting-a-server-to-process-files#i-file-limits)) for more information about the available settings

## [Scan Now](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#scan-now)

Navigate to Self Scan Workflow > Processing. Clicking the "SCAN NOW" will cause Kiosk to immediately start a Self Scan if no other scans are running. If the Kiosk UI is not running or another scan is currently in progress you will see the following error:

## [Scheduling Self Scans](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#scheduling-self-scans)

Checking the "Schedule Scan" checkbox will open up the Self Scan Scheduler where you can configure Kiosk to run a self scan at a specific time after a certain number of days or on certain weekdays.

The first option, the value for "days" must be greater than 0. Setting this value to 0 will disable scheduled self scans.

The second option, you could have multiple choices. At least a weekday must be selected.

By default, the Self Scan will not run if any other scans are currently running. This can be bypassed by checking the "Allow Self Scan to cancel any currently running scan" checkbox. WARNING: This will cancel any scan that is running during the scheduled time and you may not get the full results from the canceled scan.

## [Acknowledging Threats](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#acknowledging-threats)

Kiosk Self Scan will run a scan based on the settings in the Default Kiosk workflow. If any infected files are found, the Kiosk UI will be disabled and show a message alerting the user to contact the Kiosk Administrator. Any files marked "Infected" by this scan are displayed on the table with File Path and Threat information. Your Kiosk administrator can use this information to investigate these files if needed.

If the Kiosk is managed by My OPSWAT, that specific Kiosk instance will receive a critical health status alert to notify the Administrator.

*Health status message on My OPSWAT*

Once the Kiosk Administrator has investigated these files, the "ACKNOWLEDGE ALL THREATS" button is used to re-enable the Kiosk UI and clear the threat information from this table.

## [Monitoring Running Scans](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#monitoring-running-scans)

You can monitor the progress of the Self Scan from this same configuration page. Here you can see the current status, how many files have been scanned, and a progress bar showing the percentage complete.

Self Scans can potentially take hours to complete based on the size of the system hard drive. In the event you need to cancel a Self Scan you can use the "Cancel Sc" button. This will stop the Self Scan and free up the Kiosk UI for other scans.

## [Checking Self Scan Results](/docs/mdkiosk/v4.8.5/advanced-deployment/self-scan#checking-self-scan-results)

All threats found during a Self Scan will be displayed on the Threats table but you can also see the full scan results in the Session History page in the Logs section (Settings > Logs). All Self Scans will have "SELF SCAN -" at the beginning of their Session ID.
