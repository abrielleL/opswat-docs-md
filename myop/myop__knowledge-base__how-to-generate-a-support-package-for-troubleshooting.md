<!-- source: https://www.opswat.com/docs/myop/knowledge-base/how-to-generate-a-support-package-for-troubleshooting -->

# How to generate a support package for troubleshooting?

To help troubleshoot any issues with the virtual appliance, please follow the below instructions to generate a support package, which contains the necessary logs and configuration files.

1. Connect to the virtual appliance via SSH using the local user created at [step 5 when you deploy](/docs/myop/deployment/deployment) the My OPSWAT On-premises virtual appliance.
2. Run the below command to generate the support package.

BashCopysudo /os/prod-scripts/cent-generate-sup-package.sh

The package should be generated in the folder /home/<local user's username>/bin.

3. Use the scp utility to retrieve the support package via SSH.
