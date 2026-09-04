<!-- source: https://www.opswat.com/docs/md-ot-security/v.3.4.8/operating/anomaly-detection---protected-mode -->

# Anomaly Detection - Protected Mode

When Anomaly Detection is turned on, MetaDefender OT Security will detect any anomalous activities or behaviors of the asset or network connectivity and will generate alerts accordingly. The data that MetaDefender OT Security recorded during the learning period (assets and network connections) will be used as the baseline for anomaly detection. MetaDefender OT Security will trigger an alert when the following occurs:

- Assets that attempt to connect to the system are not in the baseline list.
- An asset is inactive for too long, exceeding the allowable threshold, which has not happened before.
- An asset is in an active state but does not communicate for a period beyond the threshold, which has not happened before.
- An asset with open ports and protocols is not in the baseline list.
- Two assets in the system communicate with each other using protocols that have not been used before.
- Two assets in the system communicate with each other on ports that have not been used before.
- Two assets in the system communicate with each other at intervals that have not occurred before.

To avoid generating unwanted alerts, ensure you have reviewed the policies for the asset and connection.

If you need to work with assets, edit settings, or perform other operations inside MetaDefender OT Security and do not want to be interrupted by alerts (which will take you to the alert screen), go to Alert Settings and disable "Make On-screen alert".

Note: Assets that are still in the learning phase will not generate alerts even if Anomaly Detection is turned on by the user.
