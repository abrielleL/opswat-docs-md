<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/operating/ot-network-security-analysis-and-forensic -->

# OT Network Security Analysis and Forensic

OT network forensics is the practice of collecting, analyzing, and reporting on data from a computer network to investigate suspicious activity or incidents. It involves capturing, preserving, and analyzing network traffic and other related data to identify and understand what happened on the network, often in the context of a cybercrime or cyberattack.

Network forensics can help you detect security breaches, identify the cause of network performance issues, and gather evidence for use in legal proceedings. Network forensics tools and techniques are used by cybersecurity professionals and law enforcement agencies to investigate and understand the details of cyber incidents.

Network forensic involves monitoring a network for anomalous traffic and identifying incidents. To not affected to current environment, you can create a new environment and import PCAP files to start analyzing.

To create new environment, you can go to the top right menu and select environments.

Then click on Create New Environment and input the environment name.

Then you can decide to keep all policies from base environment and continue.

Select PCAP file and continue.

***Note: Please make sure that you are selecting the PCAP files to import.**

Waiting for the process completed.

After importing is completed, you can start using MetaDefender OT Security.

If MetaDefender OT Security detect any incidents, alerts will be triggered immediately. The asset that having vulnerabilities will be highlighted.

You can go to asset detail to investigate further or go to Alerts page for all alerts.

User can easily monitor the network in the PCAP.

## [Environment information](/docs/md-ot-security/v.2.2.6/operating/ot-network-security-analysis-and-forensic#environment-information)

On the environment list, you can click on the PCAP files to see more detail information about the PCAP.

The information is listed as below:

- File name: PCAP file name.
- File size: PCAP file size.
- Number of packets.
- Imported time: Time that imported by MetaDefender OT Security.
- Data started at: Time that the first packet transferred in PCAP.
- Data ended at: Time that the last packet transferred in PCAP.

**Note:**

- If the base environment is having alerts, there will be an alert message on the top screen to notice to user.
- If you want to import another PCAP file, you need to switch to Live environment.
- You can select multiple PCAP files for monitoring.
- Some of dashboard widgets are not used: internal connections, connections with external host, total internal connections, protocols, active connections.
- Smart profiling can’t be used in PCAP environment.
- Allow list policies and anomaly detection feature are disabled in PCAP environment.
