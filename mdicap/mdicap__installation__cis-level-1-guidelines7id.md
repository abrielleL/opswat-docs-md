<!-- source: https://www.opswat.com/docs/mdicap/installation/cis-level-1-guidelines7id -->

# CIS Level 1 Guidelines - Linux

- Support Red Hat Enterprise [Linux 9](https://www.redhat.com/en/blog/center-internet-security-cis-compliance-red-hat-enterprise-linux-using-openscap) and,
- Ubuntu 22.04, 24.04 Pro
## [Red Hat](/docs/mdicap/installation/cis-level-1-guidelines7id#red-hat)

### [Install OpenSCAP](/docs/mdicap/installation/cis-level-1-guidelines7id#install-openscap)

BashCopyyum install openscap-scanner scap-security-guide
### [Generate a result file and a HTML report using OpenSCAP scanner tool](/docs/mdicap/installation/cis-level-1-guidelines7id#generate-a-result-file-and-a-html-report-using-openscap-scanner-tool)

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml
### [Remediation of CIS Level 1 issues](/docs/mdicap/installation/cis-level-1-guidelines7id#remediation-of-cis-level-1-issues)

Generate a remediation script based on the ssg-rhel9-ds.xml file:

BashCopyoscap xccdf generate fix --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --fix-type bash --output remediations.sh /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

And execute remediation script.

BashCopy./remediations.sh
### [Review the results after remediation](/docs/mdicap/installation/cis-level-1-guidelines7id#review-the-results-after-remediation)

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

## [Ubuntu Pro](/docs/mdicap/installation/cis-level-1-guidelines7id#ubuntu-pro)

#### [Install the UA client](/docs/mdicap/installation/cis-level-1-guidelines7id#install-the-ua-client)

BashCopysudo apt install ubuntu-advantage-tools
#### [Set up the Ubuntu Security Guide](/docs/mdicap/installation/cis-level-1-guidelines7id#set-up-the-ubuntu-security-guide)

BashCopysudo ua enable usg && sudo apt install usg
#### [Auditing an Ubuntu System for DISA-STIG compliance](/docs/mdicap/installation/cis-level-1-guidelines7id#auditing-an-ubuntu-system-for-disa-stig-compliance)

BashCopysudo usg audit cis_level1_server
#### [Applying the CIS rules to a set of systems](/docs/mdicap/installation/cis-level-1-guidelines7id#applying-the-cis-rules-to-a-set-of-systems)

BashCopysudo usg fix cis_level1_server
