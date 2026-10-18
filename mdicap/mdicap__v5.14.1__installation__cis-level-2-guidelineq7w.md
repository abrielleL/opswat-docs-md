<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/cis-level-2-guidelineq7w -->

# CIS Level 2 Guidelines - Linux

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

Support Ubuntu Pro 22.04, 24.04

For more details about the Center for Internet Security (CIS) please refer to the [**official documentation**](https://ubuntu.com/security/certifications/docs/usg/cis).

## Instruction Steps

#### Install the UA (Ubuntu Advantage) client

BashCopysudo apt update
sudo apt install ubuntu-advantage-tools
#### Set up the Ubuntu Security Guide

BashCopysudo ua enable usg
sudo apt install usg
#### Check SCAP Content Overview (Security Content Automation Protocol)

BashCopysudo oscap info /usr/share/ubuntu-scap-security-guides/1/benchmarks/ssg-ubuntu2204-ds.xml
#### Auditing an Ubuntu System for DISA-STIG Compliance

BashCopysudo usg audit cis_level2_server

The report is generated in /var/lib/usg/

#### Applying the CIS rules to a Set of Systems

There are 2 ways to apply the CIS rules:

**Method 1**: Use the usg command directly (recommend)

BashCopysudo usg fix cis_level2_server

**Method 2**: Use usg to generate a script and then run the script

BashCopysudo usg generate-fix cis_level2_server --output fix.sh

Run the fix.sh:

BashCopy./fix.sh
