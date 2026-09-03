<!-- source: https://www.opswat.com/docs/mdcore/installation/cis-level-2-guidelines -->

# CIS Level 2 - Linux Guidelines

For more details about Center for Internet Security (CIS) please refer to this [document](https://ubuntu.com/security/certifications/docs/usg/cis).

## [Instruction steps](/docs/mdcore/installation/cis-level-2-guidelines#instruction-steps)

### [Install the UA client](/docs/mdcore/installation/cis-level-2-guidelines#install-the-ua-client)

bashCopysudo apt update
sudo apt install ubuntu-advantage-tools
### [Set up the Ubuntu Security Guide](/docs/mdcore/installation/cis-level-2-guidelines#set-up-the-ubuntu-security-guide)

BashCopysudo ua enable usg
sudo apt install usg
### [Check SCAP Content Overview (Security Content Automation Protocol)](/docs/mdcore/installation/cis-level-2-guidelines#check-scap-content-overview-security-content-automation-protocol)

BashCopysudo oscap info /usr/share/ubuntu-scap-security-guides/1/benchmarks/ssg-ubuntu2204-ds.xml
### [Auditing an Ubuntu System for DISA-STIG Compliance](/docs/mdcore/installation/cis-level-2-guidelines#auditing-an-ubuntu-system-for-disa-stig-compliance)

BashCopysudo usg audit cis_level2_server

The report is generated in `/var/lib/usg/`

### [Applying the CIS rules to a set of systems](/docs/mdcore/installation/cis-level-2-guidelines#applying-the-cis-rules-to-a-set-of-systems)

There are 2 ways to apply CIS rules.

**Method 1**: directly using usg command - recommend

BashCopysudo usg fix cis_level2_server

**Method 2**: using usg to generate a script and then run the script

BashCopysudo usg generate-fix cis_level2_server --output fix.sh
#And then run
./fix.sh

**Notes:**

- A **reboot is required** to take effect after applying the fix.
- CIS Level 2 requires `/tmp` folder to be mounted in a separate partition. Please ensure that the new partition has enough disk space for MetaDefender Core to run.

### [Running fix for Ubuntu 24.04](/docs/mdcore/installation/cis-level-2-guidelines#running-fix-for-ubuntu-2404)

When generating the fix script in **Ubuntu 24.04**, there will be 2 rules (in the generated script - fix.sh) that change the permission and owner of the folder `/var/log:`

`#240: xccdf_org.ssgproject.content_rule_file_groupownerships_var_log`

`#255: xccdf_org.ssgproject.content_rule_file_ownerships_var_log`

These 2 rules will change the permission and owner of the product log also `var/log/ometascan` .

To prevent this, before running the fix script, the user needs to add `metascan` group, for example, with rule #240.

BashCopygroup="root"
find -L /var/log/ -type f -regextype posix-extended \
! -group root ! -group adm ! -group metascan \
! -name 'gdm' ! -name 'gdm3' \
! -name 'sssd' ! -name 'SSSD' \
! -name 'auth.log' \
! -name 'messages' \
! -name 'syslog' \
! -path '/var/log/apt/*' \
! -path '/var/log/gdm/*' \
! -path '/var/log/gdm3/*' \
! -path '/var/log/sssd/*' \
! -path '/var/log/[bw]tmp*' \
! -path '/var/log/cloud-init.log*' \
! -regex '.*\.journal[~]?' \
! -regex '.*/lastlog(\.[^\/]+)?$' \
! -regex '.*/localmessages(.*)' \
! -regex '.*/secure(.*)' \
! -regex '.*/waagent.log(.*)' \
-regex '.*' -exec chgrp $group {} \;

Also do the same with rule #255 to prevent update permission and the owner of `var/log/ometascan`
