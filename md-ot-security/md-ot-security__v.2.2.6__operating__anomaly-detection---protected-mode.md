<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/anomaly-detection---protected-mode -->

# Anomaly Detection - Protected Mode

When in turn on Anomaly Detection, MetaDefender OT Security will make alert if there are any abnormal activities or unauthorized behaviors in the system, including:

- Unauthorized asset connected to the system.
- An asset is in an inactive state for too long, exceeding the allowable threshold.
- An asset is in an active state but does not communicate for a period of time beyond the threshold.
- An asset that has unauthorized open ports and use unauthorized protocol on allowed ports.
- An asset that has supply chain violation.
- An asset that has CVSS score in unwanted range.
- 2 assets in the system communicating with each other using the protocol are not allowed.
- 2 assets in the system to communicate with each other on the port is not allowed.
- 2 assets in the system communicate with each other at unauthorized intervals.
- An asset that is being communicated to unwanted remote host.

To avoid generating unwanted alerts, make sure you've reviewed the policies for the asset and connection, the settings in the Asset Type Settings.

if you need to work with assets or edit settings or other operations inside MetaDefender OT Security and don't want to be interrupted by alerts (which will take you to the alert screen), just head to Alert settings and disable "Make On-screen alert".

Note: The asset that still in learning phase will not be alerted even user turn on Anomaly Detection.
