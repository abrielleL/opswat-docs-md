<!-- source: https://www.opswat.com/docs/md-ot-security/v4.0.0/operating/validate-external-ips-domains-with-threat-intelligence-database -->

# Validate external IPs/Domains with Threat Intelligence Database

For Unauthorized Connection, there is an additional feature called **Validate external IPs/Domains with Threat Intelligence Database**. To enable this feature, follow these steps:

Step 1: Policies → Connection Policies → Unauthorized Connection

Step 2: Click to settings icon

Step 3: Enable Validate external IPs/Domains with Threat Intelligence Database and save

After enabling the "Validate external IPs/Domains with Threat Intelligence Database" feature, you can create a new Unauthorized Connection policy with Threat Intelligence.

Within the policy settings, you will see the option **"Only make an alert if external IPs/Domains are found in the Threat Intelligence Database"**. This option becomes available when you select **"External Host"** for either the Source or Destination and also choose **“DNS” or “Any”** for the Protocol.

When you select the **“Only make an alert if external IPs/Domains are found in the Threat Intelligence Database”** option, the system will only create an alert under that specific circumstance.

On screen alert when the option “Only make an alert if external IPs/Domains are found in the Threat Intelligence Database” is selected

When you do not select the **"Only make an alert if external IPs/Domains are found in the Threat Intelligence Database"** option, the system will create an alert for all external hosts whether they are found in the Threat Intelligence Database or not.

On-screen Alert for External Host Found in TI Database

On-screen Alert for External Host Not Found in TI Database
