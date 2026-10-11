<!-- source: https://www.opswat.com/docs/filescan/3.2.0/installation/installation-guide -->

# AWS Installation Guide

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [**Processing Power Requirements**](/docs/filescan/3.2.0/installation/installation-guide#processing-power-requirements)

In general, we recommend at least 8 vCPUs and 32 GB RAM. Some stress tests have found the following EC2 instance types to be adequate:

- t3a.2xlarge for up to 5000 files/day and 1-5 users
- c4.4xlarge for up to 10000 files/day and 5-10 users
- c4.8xlarge for up to 25000 files/day and 10+ users

**Disc Storage Requirements**

The minimum SSD storage to get an instance up and running is 100 GB. However, while the system is in parts already configured to automatically delete local binaries (see “Retention Policy Configuration” in the User Guide), the hard disc will eventually run full. It is thus recommended to configure the webservice to use a S3 bucket and potentially move the database storage (/data/db and /data/graphdb) to an additional, external storage. Please refer to the “S3 Bucket Configuration” section of the “User Guide”.

**Launching an EC2 instance from your AMI baseline:**

Please walk through the following steps to launch an EC2 instance from your AMI baseline:

**Step #1 - Right-click your AMI and select “Launch instance from image”**

**Step #2 - Choose the appropriate instance type (see “Requirements”)**

**Step #3 - Create a security group that allows inbound SSH/HTTP/HTTPS access from your subnet (or in this case, from anywhere)**

**Step #4 - Launch your instance and wait for the state to switch from “Pending” to “Running”**

**Step #5 - The “Public IP” will be shown in the instance summary. You should be automatically redirected to HTTPS with a self-signed certificate**

**Step #6 - Setup your initial administrator. To fine-tune the system settings, head to the webservice admin panel and/or SSH into your instance and configure the Broker/Transform component or webservice according to the user guidelines.**

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
