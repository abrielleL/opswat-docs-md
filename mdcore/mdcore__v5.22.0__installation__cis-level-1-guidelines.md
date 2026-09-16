<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines -->

# CIS Level 1 - Linux Guidelines

## [Red Hat Enterprise Linux 9](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#red-hat-enterprise-linux-9)

Support Red Hat Enterprise Linux 9

For more details about Center for Internet Security (CIS) please refer to this [document](https://www.redhat.com/en/blog/center-internet-security-cis-compliance-red-hat-enterprise-linux-using-openscap)

## [Instruction steps](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#instruction-steps)

### [I. Install OpenSCAP](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#i-install-openscap)

bashCopyyum install openscap-scanner scap-security-guide
### [II. Generate a result file and a HTML report using OpenSCAP scanner tool](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#ii-generate-a-result-file-and-a-html-report-using-openscap-scanner-tool)

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml
### [III. Remediation of CIS Level 1 issues](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#iii-remediation-of-cis-level-1-issues)

Generate a remediation script based on the `ssg-rhel9-ds.xml` file:

BashCopyoscap xccdf generate fix --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --fix-type bash --output remediations.sh /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

And execute remediation script.

BashCopy./remediations.sh
### [IV. Review the results after remediation](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#iv-review-the-results-after-remediation)

BashCopyoscap xccdf eval --profile xccdf_org.ssgproject.content_profile_cis_server_l1 --results scan_results.xml --report scan_report.html /usr/share/xml/scap/ssg/content/ssg-rhel9-ds.xml

**Example**:

## [Ubuntu 22 Pro](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#ubuntu-22-pro)

### [Install the UA client](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#install-the-ua-client)

BashCopysudo apt update
sudo apt install ubuntu-advantage-tools
### [Set up the Ubuntu Security Guide](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#set-up-the-ubuntu-security-guide)

BashCopysudo ua enable usg
sudo apt install usg
### [Check SCAP Content Overview (Security Content Automation Protocol)](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#check-scap-content-overview-security-content-automation-protocol)

BashCopysudo oscap info /usr/share/ubuntu-scap-security-guides/1/benchmarks/ssg-ubuntu2204-ds.xml
### [Auditing an Ubuntu System for DISA-STIG compliance](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#auditing-an-ubuntu-system-for-disa-stig-compliance)

BashCopysudo usg audit cis_level1_server

The report is generated in `/var/lib/usg/`

### [Applying the CIS rules to a set of systems](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#applying-the-cis-rules-to-a-set-of-systems)

There are 2 ways that apply CIS rules

Method 1: directly using usg command - **recommend**

BashCopysudo usg fix cis_level1_server

Method 2: using usg to generate script and then run the script

BashCopysudo usg generate-fix cis_level1_server --output fix.sh
#And the run
./fix.sh
#### [A reboot is require to take the effect after apply the fix.](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#a-reboot-is-require-to-take-the-effect-after-apply-the-fix)

## [Notes](/docs/mdcore/v5.22.0/installation/cis-level-1-guidelines#notes)

- CIS Level 1 requires `/tmp` folder to be mounted in a separate partition. Please ensure that that new partition have enough disk space for MetaDefender Core to run.
- CIS Level 1 requires that "Ensure No World-Writable Files Exist".

  - For now, when freshly installing MetaDefender Core, all its binary files meet the requirement.
  - When installing/updating engines, some engines might create additional files for its operation, and it might violate this requirement. In this case, you need to again execute the remediation script in the step III.
