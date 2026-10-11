<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/secure-image/overview -->

# Overview

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The MetaDefender Kiosk Secure Image is a Pro-Service solution that ensures the Kiosk Operating System remains unmodified and untampered with during operation by creating a baseline of the Operating System and continuously monitoring for any changes. If any unexpected changes occur, the system halts until the alert is resolved. The MetaDefender Kiosk Secure Image is an enhancement for file integrity and regulatory compliance auditing, providing administrators with better control and visibility into their security operations.

Easy deployment methods are also available using the Secure Image Deployment Wizard. The Image provides driver package for the specific hardware of the K1001, K3000, incorporating the most stable versions of OPSWAT MetaDefender Core and MetaDefender Kiosk.

The following deployment and setup instructions for the MetaDefender Kiosk Secure Image are intended solely for customers who have purchased Secure Image as an additional Pro-Service.

## [Benefits of Secure Image](/docs/mdkiosk/v4.8.6/secure-image/overview#benefits-of-secure-image)

#### [File Integrity Monitoring (FIM)](/docs/mdkiosk/v4.8.6/secure-image/overview#file-integrity-monitoring-fim)

The Kiosk Secure Image includes a File Integrity Monitoring (FIM) feature that prevents and alerts the Kiosk administrator to any unauthorized modifications in the Kiosk installation directory.

The FIM logs an event whenever an unauthorized modification is detected and disables the Kiosk UI until a Kiosk administrator acknowledges the event in the Logs > File Integrity Monitoring section.

#### [Enhanced Group Policy](/docs/mdkiosk/v4.8.6/secure-image/overview#enhanced-group-policy)

The Kiosk Secure Image enhanced the Local Group Policy, which includes AppLocker policies to prevent unauthorized software installation and script execution.

Additionally, other Local Group Policies are implemented to enhance the security of the Kiosk hardware, including account lockout policies and more.

#### [All-in-one Package Deployment](/docs/mdkiosk/v4.8.6/secure-image/overview#all-in-one-package-deployment)

The Kiosk Secure Image includes All-In-One driver packages and automatic Windows activation for all supported hardware, eliminating the need to separate the image into different versions.

Once the deployment is complete, the driver package will be removed to conserve disk space.

#### [Quarterly Releasing](/docs/mdkiosk/v4.8.6/secure-image/overview#quarterly-releasing)

The Kiosk Secure Image will be released quarterly and will include Windows security updates, Group Policy enhancements, and more.

To apply the new release, you need to re-image the entire Kiosk Hardware OS. You can back up the MD Core and MD Kiosk configurations to restore them after re-imaging the Kiosk Hardware
