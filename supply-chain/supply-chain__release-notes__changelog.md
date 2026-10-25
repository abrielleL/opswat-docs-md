<!-- source: https://www.opswat.com/docs/supply-chain/release-notes/changelog -->

# Changelog

## Version 4.2.0

Release Date: October 14, 2026

**Highlights**

- **Cryptographic Bill of Materials (CBOM) and Quantum Safety:** MDSSC now finds the cryptographic assets in scanned content, such as algorithms and certificates. Each job, file and repository shows a quantum-safety verdict, and a new Cryptography dashboard summarizes the assets across all jobs.
- **Event-Based Scans for Harbor and Nexus Binaries:** Harbor and Nexus Binary connections can now send webhook events to MDSSC. A pushed Harbor image, or a new or updated Nexus component, starts a scan automatically.
- **Copy Remediation for Harbor and GitHub:** Copy remediation is now available for Harbor and GitHub connections.
- **Cross-Domain Transfer Improvements:** Each high-side connection mapping now selects its own import scan workflow. When the workflow has Hash Scanning on, the high side skips files it already scanned. Infected files, and files that fail to scan or are canceled, always block a transfer.

**Improvements**

- **Security Hardening:** The server validates every request field. Login errors do not reveal whether a username exists.
- **CWE Information:** The CVE table and the CVE details show CWE IDs.
- **GitHub Enterprise:** Webhook events now start scans.
- **API Keys:** Each user now has one API key. Saving a new key replaces the old one.

**Bug Fixes**

- Saving the Edit User dialog keeps the user's SSO or tenant role instead of promoting the user to Administrator
- A custom role can no longer use the "Administrator" name, so the role a user sees matches their access
- After a license is activated during onboarding, the "No active license" banner no longer appears
- MDSSC now scans the container image configuration for images without an OS
- The Upcoming Jobs table now shows scheduled jobs

## Version 4.1.1

Release Date: October 9, 2026

**Bug Fixes**

- Improved parallel scan reliability

## Version 4.1.0

Release Date: September 30, 2026

**Highlights**

- **Role-Based Access Control:** Administrators now have full control, while Read-Only Administrators can view all data without making changes. Permissions are enforced across the API and interface, with clearer messages when an action is blocked.
- **Single Sign-On:** Users can now sign in through their organization's identity provider. Identity provider groups can be mapped to MetaDefender Administrator and Read-Only Administrator roles.
- **Security Hardening:** Added brute-force protection, API rate limiting, stronger session safeguards, tighter input validation, updated HTTP security headers and TLS settings, and protections against oversized or maliciously compressed repository archives. Passwords must now contain at least 15 characters, and password reset no longer reveals whether an account exists.
- **User Session Management:** Administrators can now view and end active user sessions, immediately signing users out when a device is lost, an employee leaves, or an account may be compromised.

**Improvements**

- **JFrog Container Improvements:** JFrog container discovery now supports OCI package-type repositories. Images cached in JFrog remote repositories can be listed and scanned by digest.
- **Cross-Domain Support for Binaries:** Cross-domain transfer is now available for binary registry integrations as well as source code.
- **Smoother, More Reliable Processing:** Scan, SBOM, and package processing now use a dedicated processing service, producing results consistently across sources.

**Bug Fixes**

- The Add User form now validates the full name as it is entered and displays error messages that match the requirement
- On the high side of a cross-domain setup, container images are now unpacked when re-scanned before import, allowing the secrets policy to block images containing secrets
- The package list now retains the severity filter when changing pages
- Jira and Microsoft Teams notifications now require a Base URL, consistent with SMTP
- Onboarding now displays an actionable error if the final step fails instead of waiting indefinitely

## Version 4.0.4

Release Date: August 28, 2026

**Highlights**

- **Nexus Container Support:** Nexus Container repositories are now available as a scan source alongside existing container registries. Connect to Nexus Container registries using the new integration, triggering scans directly against your Nexus container storage.
- **Nexus Container Cross-Domain Transfers:** Transfer containers to and from Nexus Container repositories in cross-domain scenarios, completing the Nexus integration story alongside existing binary and raw-format support.
- **ECR ↔ Harbor Cross-Domain Transfers:** Cross-domain transfers now work between Amazon ECR and Harbor registries, enabling secure container movement between cloud environments. Combine this with existing GitLab and Nexus binary/container transfer capabilities to build flexible supply chain workflows across your registry infrastructure.
- **Complete Package Counts with Transitive Dependencies:** Package totals now include transitive dependencies, so the number in a report reflects everything that was scanned. Ingestion retains packages whether or not a version or ecosystem is specified, and reports load full package inventories well beyond 100 entries.
- **JFrog Container Webhooks:** The JFrog container integration now supports event-based scanning via webhooks. New or updated container artifacts trigger scanning automatically, enabling continuous monitoring.

**Improvements**

- **Expanded SBOM Exports:** SBOM PDF exports now include transitive dependencies, giving you the complete dependency tree in a single document. CycloneDX exports carry end-of-life and criticality properties for each component along with the root dependency relationship.
- **Cross-Domain Scan Results Visibility :** High-side analyze logs now include direct redirect links to their corresponding reports, so you can move from a cross-domain transfer straight to the report without manual navigation.
- **Notification and Interface Refinements:** Improved error handling for unconfigured cross-domain settings, better SBOM completion on TLS setups, and cleaner onboarding flows.

**Bug Fixes**

- SBOM exports in CycloneDX and SPDX formats no longer drop packages whose version could not be resolved
- PDF and CSV exports now report the correct package total for direct-file SBOM scans instead of double counting
- CVE search now matches the "Repositories With Issues" column
- TLS certificate validation for SBOM completion now works correctly when `MD_CORE_CERTIFICATE_VALIDATION=IgnoreAllErrors` is set
- Global cross-domain config endpoints now return clean 200 responses on unconfigured installs instead of 404s
- Archive content views on direct SBOM scans now display properly

## Version 4.0.0

Release Date: July 20, 2026

**Highlights**

- **New User Interface:** The web interface has been rebuilt from the ground up for a faster, clearer, and more consistent experience. Navigation, dashboards, and result views have been reorganized to surface the information that matters most and to make large repositories easier to explore.
- **Jobs Replacing Scans:** The "Scan" concept has been replaced by Jobs, a more flexible unit of work that groups the processing of a repository or source into a single, trackable activity. Jobs provide clearer status, history, and results, and lay the foundation for the platform's expanded workflows.
- **Risk Score For Repositories:** Repositories now display an aggregated risk score, giving teams an at-a-glance measure of overall security posture. The score consolidates findings across a repository so you can prioritize the sources that need attention first.
- **Security Suggestions:** The platform now provides Security Suggestions - actionable recommendations that help you remediate detected issues. Suggestions turn raw findings into clear next steps, reducing the time from detection to resolution.
- **JFrog Container Webhooks:** The JFrog container integration now supports event-based scanning via webhooks. New or updated container artifacts trigger scanning automatically, enabling continuous monitoring.

**Improvements**

- **New SBOM PDF Export with More Fields:** SBOM PDF export has been expanded to include additional fields, producing a richer, more complete software bill of materials. The enhanced report makes it easier to share comprehensive component and dependency information with stakeholders and auditors.
- **CSV Exports for Packages :** Package inventories can now be exported to CSV, making it simple to analyze, filter, and share package data outside the platform or feed it into other tools and reporting pipelines.
- **Container Layer Scanning and Skip by Hash:** Container images are now scanned layer by layer, with previously scanned layers skipped by hash. This improves the granularity of container findings while avoiding redundant work, delivering faster scans across images that share common layers.

## Version 3.3.1

Release Date: May 19, 2026

**Highlights**

- **Harbor Registry Integration:** Added support for integrating with Harbor Registry, enabling scanning of container images for vulnerabilities, malware, and compliance issues.
- **Cross Instance Copy Remediation for JFrog Containers:** Added support for remediating container image vulnerabilities during cross-instance copy operations, ensuring consistent policy enforcement across registries.
- **Dashboard Statistics Options:** Added an environment configuration option to include or exclude direct file scans from dashboard statistics.
- **Advanced Package and Archive Processing:** Enhanced processing for complex package and archive formats to improve ingestion reliability and stability for multi-layered archives.

**Improvements**

- **Dashboard statistics options:** Added configuration to include or exclude direct file scans from dashboard statistics for more tailored reporting.
- **Advanced package and archive processing:** Improved ingestion pipeline reliability when processing complex package and archive formats.

**Bug Fixes**

- **Report deletion UI state:** Fixed an issue where report details remained visible in the interface after a successful deletion request.
- **Weekly schedule re-queue:** Fixed an issue that prevented weekly scheduled scans from being automatically re-queued for the next occurrence.

## Version 3.3.0

Release Date: April 8, 2026

**Highlights**

- **Cross Domain Transfer (V2 Beta UI):** Added support for securely transferring scanned data from Low Side to High Side environments, with optional Data Diode support for strictly segmented networks.
- **Sonatype Nexus Repository Integration:** Added support for connecting to on-premises Nexus repositories to manage and scan stored binary artifacts for vulnerabilities and compliance issues.
- **Gitea Integration:** Added support for connecting Gitea instances and enabling automated scanning of source code repositories for vulnerabilities and compliance issues.
- **Offline License Activation:** Added offline license activation, allowing licenses to be generated outside the product environment and uploaded to complete activation. After upload, the UI displays key license details, including repository counts.

**Improvements**

- **Dashboard vulnerability trends:** Added a chart that visualizes vulnerability trends over time.
- **New SBOM fields:** Added CVSS score fields for CVEs.

**Bug Fixes**

- **External Logger Server UI consistency:** Fixed UI inconsistencies related to the External Logger Server configuration.
- **GitLab repository visibility detection:** Fixed incorrect identification of private vs public repositories in GitLab.
- **Connection credential update refresh:** Fixed an issue where updating connection credentials did not refresh and show the updated repositories.
- **CycloneDX for binary services:** Fixed CycloneDX report generation for binary service connections.
- **Bitbucket inventory connection creation:** Fixed an issue that prevented adding Bitbucket Cloud or Bitbucket Data Center connections to Inventory.

## Version 3.2.0

Release Date: February 25, 2026

**Highlights**

- **Performant Pagination for SVN and Quay Connections:** Pagination for SVN and Quay now uses cursor-based pagination for improving speed and efficiency, reducing resource usage when browsing large datasets.
- **Scan Schedule Dispersion mechanism:** The application creates a window in time for distributing the scans along a schedule. Scans start in batches along the allocated time, which increases performance and completion rates of scheduled scans.
- **Repository Count on Inventory page:** The Inventory page now displays the total number of repositories for the connection, giving users immediate visibility to their connection's repository data.

**Improvements**

- **Workflow Creation:** Workflow creation no longer requires loading all branches at once. Branches are now fetched in smaller batches to reduce timeout risks.
- **Repositories scan order prioritization:** The application now orders repositories in Inventory by their last scan date. This grants easy access to latest scanned repositories and acts like a summary of your latest scanned repositories for a connection.
- **Parallel Scan Stability Enhancement:** Improved handling of high-volume parallel scans, enhancing overall reliability and throughput under intensive workloads.
- **Cleanup job for files:** Temporary files from completed, cancelled, or failed scans are now automatically cleaned up to prevent disk space accumulation and improve system reliability.
- **New Environment Variable for gRPC Proxy Channel control:** The environment variable controls whether gRPC channels route connections through the system proxy, providing greater flexibility over gRPC networking behavior.

**Bug Fixes**

- **Workflow settings persistence:** Workflow settings for hash scanning, scan schedules, and remediations are now reliably preserved across all workflow update scenarios.
- **Direct scan with default workflow:** Direct file scanning works with the default workflow.

## Version 3.1.2

Release Date: January 15, 2026

**Improvements**

- **CSV Reporting:** Enhanced reporting capabilities to support CSV file generation, ensuring compliance with reporting requirements.
- **Dashboard Performance Enhancement:** Optimized Dashboard performance to improve responsiveness and scalability under high-volume usage.

**Bug Fixes**

- **Scan Schedule Stability Enhancement:** Resolved a critical scheduling issue occurring under high system load, where scans involving a large number of repositories could become blocked and remain indefinitely in an *In Progress* state. The scheduling and execution logic has been optimized to ensure reliable scan completion and improved stability during high-volume, concurrent scan operations.
- **Scan Instance Update:** Editing of scan instances is now fully supported

## Version 3.1.1

Release Date: December 24, 2025

**Highlights**

- Direct File Scanning: Users can now drag and drop files directly into the web interface, where they are automatically scanned without any additional steps.

## Version 3.1.0

Release Date: December 10, 2025

**Improvements**

- **Microsoft Teams Remediation:** Enabled a new integration that sends scan reports directly to Microsoft Teams channels. This allows teams to receive immediate insights.
- **New Azure DevOps Service:** Expanded source code repository support to include **Azure DevOps**. Users can now connect and scan repositories hosted within the Azure DevOps environment.
- **SPDX 3.0 Reporting:** Updated reporting capabilities to include support for the **SPDX 3.0**, ensuring compliance with the latest Software Bill of Materials (SBOM) specifications.

**Bug Fixes**

- **Performance Optimization:** Addressed general system performance issues to ensure faster load times and smoother operation during high-volume usage.
- **Pagination Logic:** Resolved specific performance bottlenecks related to page navigation, ensuring smoother transitions.
- **Bitbucket Integration:** Fixed an issue where Bitbucket branches were not displaying correctly. Pagination for Bitbucket repositories now functions as expected.
- **Amazon ECR Connectivity:** Corrected a bug that prevented public repositories on **Amazon ECR** from displaying.
- **Jira Vulnerability Sync:** Resolved a discrepancy where Jira tickets displayed an incorrect count of vulnerabilities. The ticket data now accurately matches the scan results.
- **Password Reset:**  Resolved an issue that was blocking some users from resetting their passwords. Account recovery now works as expected.

## Version 3.0.1

Release date: November 13, 2025

This is a hotfix release addressing critical issues from v3.0.0 and introducing minor enhancements.

**Improvements**

- Added a Scan Cleanup feature on the Reports page, allowing users to remove old scans based on a defined timeframe. This helps manage storage and maintain a cleaner scan history.
- SMTP email notifications now include the SBOM PDF as an attachment, providing recipients with immediate access to comprehensive scan reports.
- Updated MDSSC to support SSL certificate–based MDCore instances, enhancing secure communication between MDSSC and MetaDefender Core deployments.

**Bug fixes**

- Resolved issue preventing SVN connection updates from functioning correctly. Users can now properly modify SVN repository credentials and settings.
- Corrected problem with SMTP configuration updates not applying as expected. Email notification settings now save and apply correctly.
- Fixed inconsistent behavior of the Scan Diff feature for GitLab and GitHub integrations, ensuring reliable differential scanning across both platforms.

## Version 3.0.0

Release date: October 30th, 2025

**Highlights**

- **PostgreSQL Database Migration** – MDSSC now uses PostgreSQL as its primary database, replacing MongoDB for improved performance, scalability, and data reliability.
- **Source Code Differential Scanning** – Introduced a new diff scanning feature that analyzes only changes between commits, significantly reducing scan time and improving efficiency.
- **Default Workflow for Immediate Scanning** – A ready-to-use default workflow is now available out-of-the-box, enabling users to start scanning repositories immediately without manual configuration.
- **AWS ECR GovCloud Support** – Added support for AWS Elastic Container Registry (ECR) GovCloud to serve customers operating in U.S. Government environments.
- **Bitbucket Cloud Token Authentication** – Bitbucket Cloud integration now supports API token-based authentication for enhanced security and compliance.
- **Archive Extraction for Repository Scans** – Enabled archive extraction during Bitbucket and GitLab scans for comprehensive analysis of compressed source code and dependencies.
- **Encrypted Sensitive Customer Data** – Sensitive customer information is now encrypted in the database to meet stricter data protection and compliance standards.
- **New Cards View for Top Issues** – Redesigned Cards View UI with visual prioritization to enable faster triage and decision-making.

**Improvements**

- Optimized database queries following PostgreSQL migration.
- Updated UI components for faster navigation and improved accessibility.
- Refined system health monitoring and logging capabilities.

**Bug fixes**

- Fixed workflow initialization issues when creating new scans.
- Corrected GitLab integration timeout handling.
- Updated API documentation to reflect new PostgreSQL data structure.
- Added migration guide from MongoDB to PostgreSQL.

## Version 2.5.4

Release date: September 4th, 2025

**Highlights**

- Cross‑JFrog Copy Remediation
- GitHub Webhook Testing Support
- Dashboard Redesign (Phase 1) & Updated components
- MetaDefender Cloud Scan Support
- External Logger (Syslog) Support

**Bug fixes**

- Implemented rate limiting across APIs to mitigate abuse and improve security posture.

## Version 2.5.3

Release date: August 7th, 2025

**Highlights**

- **JFrog real‑time scanning** with remediation (copy/delete/email), webhook tests, and cert toggle
- **SBOM PDF** updated with supplier info, release dates, and clickable package links
- Refreshed UI: modernized **login/register screens** and license details view

**Bug fixes**

- Implemented rate limiting across APIs to mitigate abuse
- Overall stability and UI interaction improvements

## Version 2.5.2

Release date: July 9th, 2025

**Highlights**

- Manifest v1 Image Scanning
- Transitive Dependencies
- Package Version History States
- Custom Package Labels
- Detailed PDF Reports
- New Recommended Fixed Version

**Bug fixes**

- Resolved data inconsistency issues when upgrading to a new version.
- Corrected the support package name display.
- PDF export now supports filters for exported Report.

## Version 2.5.1

Release date: May 30th, 2025

**Highlights**

- SBOM Enhancements and PDF Export
- Webhook Support for Bitbucket
- Improved Bitbucket and GitHub Integration
- Added CycloneDX Metadata

**Bug fixes**

- Some pages now include spinners to improve loading feedback. Minor layout and interaction bugs.
- Email reports have been cleaned up for better readability.

## Version 2.5.0

Release date:  April 16th, 2025

**Highlights**

- Enhanced Repository and Package Reporting
- CycloneDX SBOM Export for Scan Results
- JFrog Binary and GitLab Webhook Integration
- Expanded Remediation Actions in JFrog Binary

**Bug fixes**

- Improved internal repository ID handling that was causing scan reports to show up for incorrect connections with same repository
- Added various internal error handling improvements that caused certain operations and scans to fail.

## Version 2.4.2

Release date: February 28th, 2025

**Highlights**

- Integration of SVN support
- Added masking over API Key for Scan Instance
- Added delete button for reports
- GitHub connection registration guide updated

**Bug fixes**

- Resolved several issues in UI and improved error handling mechanisms

## Version 2.4.1

Release date: February 6th, 2024

**Highlights**

- Archive files handling for SBOM
- Enhanced Jira Connection security
- Added delete action for scan reports
- Configurable GitLab SSL Certificate Validation Bypass

**Bug fixes**

- Resolved UI Issues in Dashboard and Reports Modules

## Version 2.4.0

Release date: December 18th, 2024

**Highlights**

- New source code service integration: GitLab
- New Notification option: Jira Connections
- Performance improvement, by the added support of source code services pagination

**Bug fixes**

- Resolved UI Issues in Workflow and Inventory Modules

## Version 2.3.2

Release date: November 5, 2024

**Highlights**

- New "Soft Deletion" remediation action for GitHub and Bitbucket

**Bug fixes**

- Fixed incorrect data in the pdf reports sent via email notifications
- Improved scan progress bar display and workflow refresh in UI
- Adjusted audit log message levels for accuracy

## Version 2.3.1

Release date: September 25, 2024

**Highlights**

- SBOM: License Risk Detection
- Email Address Update Capability

**Bug fixes**

- Bitbucket Cloud Integration: archive processing for repositories to bypass rate limiting, enhancing data retrieval efficiency
- Significant improvements to screen loading speeds, streamlining user interactions and responsiveness

## Version 2.3.0

Release date: August 28, 2024

**Highlights**

- New Source Code Integration: Bitbucket Cloud and Bitbucket Data Center (On-Premises)
- New Container Registry Integration: Azure Container Registry (ACR)
- Refreshed Dashboard UI and User Experience

**Bug fixes**

- Resolved UI Issues in Reports and Inventory Modules

## Version 2.2.0

Release date: July 15, 2024

**Highlights**

- Support for Artifactory. We are excited to announce our new service integration: **JFrog Binary**. This integration allows you to scan artifacts from a JFrog Artifactory server, both cloud-based and on-premises. All existing options available for other services are fully supported for JFrog Binary as well.
- New service integration: **JFrog Containers**
- Branch Configuration for Source Code Scanning
- GitHub Enterprise Support for Source Code Scanning
- Basic Configuration and Enrollment with myOPSWAT

**Bug fixes**

- Enhanced logging capabilities with log rotation and retention, ensuring better management and access to log data.
- Improved handling for expired service credentials. You will now receive visual aids prompting you to reconnect.
- Upgraded RabbitMQ to version 3.13, providing the latest features and security enhancements.

## Version 2.1.0

Release date: April 2, 2024

**Highlights**

- Users can now edit their GitHub connection settings to prevent scanning interruptions due to token expiration
- We're excited to introduce a new feature on the dashboard that displays a list of upcoming scheduled scans. This enhancement provides users with greater visibility and organization of their scanning schedule, allowing for better planning and management of resources. Stay on top of your scanning tasks effortlessly with this convenient addition to the dashboard.
- When reviewing scan results, users will have immediate access to the fixed version for each package identified. This enhancement streamlines the remediation process, enabling users to quickly identify and implement necessary updates.
- We've added a quick onboarding tutorial for first-time users, making it easier for them to get started with our project. This step-by-step guide helps users familiarize themselves with our platform's key features quickly, ensuring a smoother initial experience and faster adoption.

**Bug fixes**

- Improved the display for failed scans to provide clearer feedback to users.
- The issue regarding the audit table row not expanding correctly has been addressed and resolved.
- The issue of data overflowing out of the defined cell in the scan report has been resolved.
- The update password button occasionally remaining greyed out inadvertently has been addressed, ensuring consistent functionality for users.
- Users were inadvertently able to select an empty scan pool for their workflow, but this issue has now been corrected to prevent such occurrences.
- Enhanced error handling has been implemented to address cases where users encounter missing permissions while adding an Amazon ECR connection, ensuring smoother integration processes.

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
