<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/cis-os-hardening-guidelines -->

# CIS OS Hardening Guidelines

MetaDefender Aether is compatible with installations on operating systems hardened to CIS Level 1 or Level 2 standards: <https://www.cisecurity.org/cis-benchmarks>

Warning

Please note that CIS Level 1 or Level 2 hardening is not yet available on **Ubuntu 24.04**

Here you can find a more user-friendly description of the relevant changes applied during hardening:

- [Ubuntu 22.04 Level 1 Audit](https://www.tenable.com/audits/CIS_Ubuntu_Linux_22.04_LTS_v2.0.0_L1_Server)
- [Ubuntu 22.04 Level 2 Audit](https://www.tenable.com/audits/CIS_Ubuntu_Linux_22.04_LTS_v2.0.0_L2_Server)

This documentation provides some example instructions to harden an Ubuntu 22.04 operating system.

### [Hardening steps](/docs/filescan/3.1.1/installation/cis-os-hardening-guidelines#hardening-steps)

OpenSCAP will be utilized for the hardening process. For more details about the tool, please refer to the official OpenSCAP website: <https://www.open-scap.org>

Install the OpenSCAP tool on your system.

BashCopysudo apt install libopenscap8 -y

Additionally, download the relevant security guides, which contain practical hardening advice and links to compliance requirements in order to ease deployment activities such as certification and accreditation.

You can find the installation step on the OpenSCAP website. <https://www.open-scap.org/security-policies/scap-security-guide/#install>

BashCopyapt install ssg-base ssg-debderived ssg-debian ssg-nondebian ssg-applicationsWarning

The installation may fail because the ssg packages are currently unavailable in the Ubuntu 22.04 repositories.

In this case, the relevant ssg can be manually downloaded from the ComplianceAsCode repository.

<https://github.com/ComplianceAsCode/content/releases/tag/v0.1.74>

Example script to download the pre-built security guide and transfer the relevant files to the OSCAP target location

BashCopywget https://github.com/ComplianceAsCode/content/releases/download/v0.1.74/scap-security-guide-0.1.74.zip
unzip scap-security-guide-0.1.74.zip
rm scap-security-guide-0.1.74.zip
mkdir -p /usr/share/xml/scap/ssg/content/
cp scap-security-guide-0.1.74/ssg-ubuntu2204* /usr/share/xml/scap/ssg/content/

Verify the installation by running the following command:

BashCopysudo oscap --v

As a result, you should see an output similar to the following:

Run an evaluation on the system to generate a baseline report, which will be used to create the remediation script. Make sure to **save the report** so you can compare the results after the hardening process.

Use the following command to run the evaluation and save the results in both XML and HTML formats:

BashCopysudo oscap xccdf eval --results result.xml --report report.html --profile xccdf_org.ssgproject.content_profile_cis_level2_server /usr/share/xml/scap/ssg/content/ssg-ubuntu2204-ds.xml

Generate the remediation script based on the `report.xml` file:

BashCopysudo oscap xccdf generate fix --fix-type bash --output my-remediation-script.sh --result-id xccdf_org.open-scap_testresult_xccdf_org.ssgproject.content_profile_cis_level2_server result.xml

Execute the remediation script:

BashCopysudo chmod o+x my-remediation-script.sh
sudo ./my-remediation-script.shInfo

The script will address many issues. However, please note that some findings may still require manual intervention.

### [Review hardening results](/docs/filescan/3.1.1/installation/cis-os-hardening-guidelines#review-hardening-results)

To review the changes implemented by the remediation script, run the evaluation again. Make sure to use different file names for the XML and HTML reports to facilitate comparison of the results.

BashCopysudo oscap xccdf eval --results result-post.xml --report report-post.html --profile xccdf_org.ssgproject.content_profile_cis_level2_server /usr/share/xml/scap/ssg/content/ssg-ubuntu2204-ds.xmlInfo

When comparing the results, you should observe that cases where a rule evaluation previously resulted in a failure are now marked as passed.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
