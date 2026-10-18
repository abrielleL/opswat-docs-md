<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/cis-level-1-guidelines7id -->

# CIS Level 1 Guidelines - Linux

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

- Support Red Hat Enterprise [Linux 9](https://www.redhat.com/en/blog/center-internet-security-cis-compliance-red-hat-enterprise-linux-using-openscap) and,
- Ubuntu 22.04, 24.04 Pro
## Red Hat

### Install OpenSCAP

BashCopyyum install openscap-scanner scap-security-guide
### Generate a result file and a HTML report using OpenSCAP scanner tool

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml
### Remediation of CIS Level 1 issues

Generate a remediation script based on the ssg-rhel9-ds.xml file:

BashCopyoscap xccdf generate fix --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --fix-type bash --output remediations.sh /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

And execute remediation script.

BashCopy./remediations.sh
### Review the results after remediation

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

## Ubuntu Pro

#### Install the UA client

BashCopysudo apt install ubuntu-advantage-tools
#### Set up the Ubuntu Security Guide

BashCopysudo ua enable usg && sudo apt install usg
#### Auditing an Ubuntu System for DISA-STIG compliance

BashCopysudo usg audit cis_level1_server
#### Applying the CIS rules to a set of systems

BashCopysudo usg fix cis_level1_server
