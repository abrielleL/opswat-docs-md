<!-- source: https://www.opswat.com/docs/mdcluster/release-notes/mddc-archived-release-notes -->

# Archived release notes

## [Version v2.8.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v280)

Release Date: 30 July 2026

**Kubernetes deployment**

MetaDefender Cluster can now be deployed and operated on Kubernetes, enabling scalable, cloud-native deployments across modern infrastructure.

**High availability**

MetaDefender Cluster now supports high-availability deployments on Kubernetes, with HA deployment options for PostgreSQL, RabbitMQ, Redis and MetaDefender Cluster File Storage.

**Staged upgrades**

MetaDefender Cluster now supports staged upgrades through separate Helm charts for platform services and worker instances, reducing service disruption during upgrades.

**Official Docker images**

Official Docker images are now available for all MetaDefender Cluster services, simplifying containerized deployments.

**Graceful worker shutdown**

MetaDefender Cluster Worker instances running on Kubernetes now complete in-progress processing before shutting down, helping prevent interrupted scans during scaling and upgrades.

**Terraform deployment**

Infrastructure as Code (IaC) support has been introduced using Terraform, allowing consistent deployment of MetaDefender Cluster across AWS, Microsoft Azure, and Google Cloud Platform. Production-ready Terraform templates are included to simplify provisioning and deployment.

**Further Enhancements**

- Improved container resource monitoring by accurately reporting Docker and Kubernetes CPU and memory limits instead of host resources.
- Improved stability for long-running service operations by preventing idle network timeouts through firewalls and load balancers.

**Security Enhancements**

- Upgraded library for vulnerability fixes: PostgreSQL to 18, NGINX to 1.30.4, OpenSSL to 3.5.7, SQLite to 3.53.3, 7-Zip to 26.02, yaml-cpp to 0.9.0, nghttp2 to 1.69.0, and Angular to 20.x.

**RESTful API**

- A new GET `/readyz` endpoint is available to allow Kubernetes and external orchestration systems to determine whether a service is ready to receive traffic.

**Bug Fixed**

- Fixed an issue where the GET `/file` API incorrectly returned **404 Not Found** for files scanned by users that had later been deleted. The API now returns the scan result with an empty user field.

## [Version v2.7.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v270)

Release Date: 30 June 2026

**Active Directory (AD) and LDAP Authentication**

MD Cluster 2.7.0 now supports user authentication through Active Directory (AD) and LDAP. Users authenticated via AD/LDAP can also generate and manage their own API keys.

**Service Connection Configuration via Ignition File**

MD Cluster 2.7.0 allows service connections to be configured through the Ignition file during MD Cluster Control Center installation, simplifying automated deployments and initial setup.

**OPSWAT AI Content Inspector Integration**

MD Cluster 2.7.0 introduces integration with OPSWAT AI Content Inspector, enabling AI-powered content analysis as part of the MD Cluster workflow.

**Further Enhancements**

- Service Connection Import via YAML
- Processing History Filtering by File Extension
- Certificate Renaming
- Heartbeat Support for All Services

**Security Enhancements**

- Introduced a more secure API key format. API keys are now 36 hexadecimal characters (`0-9`, `a-f`), containing at least 10 letters, at least 10 digits, and no more than three consecutive characters of the same type.
- Fixed a potential denial-of-service issue caused by unlimited worker addition.
- Restricted local file paths when reading certificates to improve security.
- Fixed potential SQL injection vulnerabilities.
- Restricted callback destinations to help prevent unauthorized callback requests.
- Upgraded NGINX to v1.30.3.
- Upgraded OpenSSL to v3.5.7.

**RESTful API**

- Added support for API endpoints to retrieve blocked leaves: GET [/file/{data_id}/blocked-leaves](/docs/mdcluster/api-gateway#retrieveblockedleaffile) and GET [/hash/{md5|sha1|sha256|sha512}/blocked-leaves](/docs/mdcluster/api-gateway#retrieveblockedleaffilebyhash).
- The POST [/file](/docs/mdcluster/api-gateway#fileanalysispost) API endpoint now accepts only requests with the `application/octet-stream` content type.

**Bug Fixes**

- Fixed an issue where a deployed MD Core could fail to start after being forcefully stopped or when its master Nginx process was terminated.
- Fixed an issue that could cause distributed archive extraction to hang when processing certain archive files.
- Fixed an issue where MD Cluster Control Center and Identity Service could fail to start if the PostgreSQL password contained special characters.

## [Version v2.6.1](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v261)

Release Date: 21 May 2026

**Cross-Instance Processing Result Reuse by File Hash**

MD Cluster 2.6.1 supports cross-instance processing result reuse by file hash. When the same file is submitted, an MD Core instance can reuse existing processing results instead of processing the file again. If the original file is still being processed, the requesting instance waits for completion before reusing the result. This helps reduce bandwidth usage and improves resource efficiency, especially for complex tasks.

**Remote Upgrade Support for MD Cluster Worker**

MD Cluster 2.6.1 now supports remote upgrades for MD Cluster Workers directly from Control Center. System administrators can trigger upgrades centrally, and all connected MD Cluster Workers will be upgraded automatically without requiring manual intervention.

**RESTful API**

- Added `blocklisted_reason` and `allowlisted_reason` fields to the response of GET `/file/{data_id}`, `{% badge type="info" text="GET" /%}/file/batch/{batch_id}` and GET `/hash/{md5|sha1|sha256|sha512}`.
- Added support for the `{% badge type="info" text="GET" /%}/file/{data-id}/extraction-errors` API endpoint.

**Further Enhancements**

- Search Executive Reports by Workflow Rule Name
- Separate Protected File Verdicts
- Extraction Issue Reporting
- Archive Nesting Visibility
- Two-Year Executive Report Access

**Security Enhancements**

- Upgraded NGINX to v1.30.1.
- Upgraded PostgreSQL to v14.23.
- Access to available rules, password policy settings, and active performance reports in MD Cluster Control Center can now be restricted based on user permissions.

**Bug fixes**

- Fixed an issue where MD Core support packages larger than 4 GB could not be generated.
- Fixed an issue that prevented an engine from being disabled on MD Cluster Control Center while it was waiting for installation in MD Core instance.
- Fixed an issue where passwords were not retained in files generated through distributed compression.

## [Version v2.6.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v260)

Release Date: 15 April 2026

**Centralized engine configuration for MetaDefender Core**

System administrators can now manage engine settings for all MD Core instances from a single location. They can enable, disable, or remove engines centrally, and any changes are automatically synchronized across all instances.

**Simplified MetaDefender Worker installation**

MetaDefender Cluster Worker is now bundled with MetaDefender Cluster Control Center. Users can install MetaDefender Cluster Worker through a single script available in Control Center.

**Configurable minimum engine and MD Core instance requirements**

Allow users to configure the minimum number of active MetaDefender Core, active AV engines, and required engines. This gives administrators more control over system readiness.

**Redesigned distributed extraction flow**

The distributed extraction flow has been redesigned to make better use of system resources while improving overall product stability.

**Distributed compression**

Distributed compression is now supported in MetaDefender Cluster, allowing archive files to be generated across multiple MetaDefender Core instances.

**Further Enhancements**

- Faster MetaDefender Cluster File Storage
- Faster executive report retrieval
- Custom installation directory support
- Display of Total Extracted File Size
- Display of stop reason
- Improved audit log search and filtering
- File size filter for Processing History
- MetaDefender Aether integration

**Security Enhancements**

- Upgraded library for vulnerability fixes: Nginx 1.29.7, 7zip 26.0.0, OpenSSL 3.5.6, Sqlite 3.51.2,PostgreSQL 14.22, zlib 1.3.2, Nghttp2 1.68.1, tikio-rs/bytes 1.11.1, quinn-proto 0.11.14, and webpki 0.103.10.
- Address a high-severity SQL injection vulnerability in the Control Center search functionality. The fix ensures that all search inputs are properly validated and handled using secure query mechanisms to prevent injection attacks.
- Fix a Denial-of-Service (DoS) vulnerability affecting endpoints that support resource listing and allow clients to specify the number of resources to be returned in a single request.

**Bug fixes**

- Fix an issue where some fields were missing in the JSON response of GET `/file/{batch_id}` when the request was returned through MetaDefender Cluster API Gateway.
- Fix a potential MetaDefender Cluster Worker crash that could occur when DEBUG logging is enabled.
- Fix an issue that prevented Proactive DLP engine from being deployed on Windows due to the long file path limitation.

## [Version v2.5.2](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v252)

Release Date: 26 January 2026

**RESTful API**

- Added support for the `current_finished_files` field in the responses of GET `/batch/{batch_id}` and GET `/file/{batch_id}`.

**Further Enhancements**

- Optimized data lake queries to speed up retrieval of processing history records.
- Prevented multi-platform MD Core deployment to ensure consistent processing results.
- Added IPv6 support for essential MD Cluster services to improve modern network compatibility.
- Enabled fetching and installing OPSWAT Predictive Alin AI packages on MD Core for automated engine setup.

**Security Enhancements**

- Upgraded Nginx to 1.29.4 for vulnerability fixes.
- Addressed a security vulnerability that could permit unauthenticated remote code execution within MD Cluster Control Center and API Gateway.
- Addressed a vulnerability in user management operations that could allow SQL injection and potentially cause Denial of Service.

**Bug Fixes**

- Corrected inaccurate display of outdated scan engines in System Health.
- Resolved a problem that allowed selection of the License Management Service Activation rule even when using an invalid token.
- Fixed an issue where an MD Core instance’s active license could become permanently inactive after switching to a different license.
- Corrected a problem that allowed system admins to deactivate an online license that had already expired.

## [Version v2.5.1](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v251)

Release Date: 16 December 2025

**Support licensing with License Management Server (LMS)**

New licensing management model for MetaDefender Cluster to allow license management server to manage the product's license status.

**Further Enhancements**

- Improve the performance of fetching processing history.
- Support sorting processing history by duration.
- Enhance product stability.

**Security Enhancements**

Upgraded library for vulnerability fixes:

- PostgreSQL v14.20

**Bug Fixes**

- Fixed an issue where certain archive file remained stuck in the in-progress state.
- Fixed an issue that led to the process start time of batch is invalid.
- Fixed a crash in MD Cluster Control Center when adding a worker using IPv6.
- Addressed incorrect status reporting of MD Cluster Worker when a machine was unexpectedly powered off.
- Fixed an issue where the MD Cluster Worker was unable to upgrade its hosted MD Core.

## [Version v2.5.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v250)

Release Date: 30 October 2025

**MetaDefender Cluster license**

New licensing model requires a MetaDefender Cluster license.

**Chart for in-queue objects in System Activity**

A new chart in System Activity shows the overall count of objects pending processing.

**Dedicated callback service**

A new optional service is introduced to dedicate sending the results of finished scan requests to the webhook server. The service can be scaled out easily and upgraded seamlessly.

**Engine package update initiated by folder monitoring**

Modification of engine packages in a given folder can be monitored and notified to MetaDefender Core instances for engine updates.

**Time availability for scan request acceptance**

MetaDefender Cluster API Gateway will accept scanning requests from clients during a pre-define time windows.

**Workflow priority**

MetaDefender Cluster Control Center allows system administrators to configure the priority of a specific workflow.

---

**RESTful API**

MetaDefender Cluster API Gateway:

- Introduce `metadata` request header to include vulnerability details in the response of GET `/batch/{batch_id}/certificate` API.
- Introduce GET`/file/webhook/{data_id}` API to retrieve the callback status of a scan request using `data_id`.
- Support `callbackurl` header in requests to POST `/file` API.
- Include callback service status in GET `/readyz` API.

MetaDefender Cluster Control Center:

- Introduce PUT and GET `/admin/config/sessioncookie` to modify and get session cookie attributes.
- Drop support for `license_id` field in POST `/admin/worker/deploy` API.
- Support callback service installer for POST `/admin/installer` API.
- Introduce a new `callback-service` type for the APIs: POST `/admin/worker/deploy`, POST `/admin/worker/upgrade` and GET `/admin/worker/upgrade/version`.

---

**Further Enhancements**

- Improve the performance of gathering materials for the executive report.
- Capability to configure the communication port of MetaDefender Core during deployment.
- Support instance name filtering for processing history exported in STIX/CSV format.
- Include metrics for waiting time related to file type detection in the executive report.

---

**Security Enhancements**

Upgraded library for vulnerability fixes:

- OpenSSL 3.5.4

**Bug Fixes**

- Fixed the issue that led to the disappearance of MetaDefender Core instances from Instance Activity during high load.
- Fixed the issue that led to MetaDefender Core instances losing their licenses after the upgrade.
- Fixed the issue that caused GET `/file/{data_id}` API to return a zero `upload_time`.
- Fixed the issue that led to the omission of scan results for files within a batch when a filter was applied.

## [Version v2.4.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v240)

Release Date: 30 September 2025

**Export scan result in JSON format**

From MetaDefender Cluster (MD Cluster) Control Center, users can export scan result in JSON format.

**Export processing history in STIX or CSV format**

Processing history can be exported in STIX or CSV format from MD Cluster Control Center.

**Remove abandoned module packages**

Abandoned module packages can be selected and removed on web console of Control Center.

**Customize the system health check**

System administrators can enable the health check option and set the minimum number of required MetaDefender Core instances in the Health Check settings of the MD Cluster Control Center.

---

**RESTful API**

- Introduce a new API endpoint in MetaDefender Cluster API Gateway to verity if the system is ready for new scan requests GET `/readyz`.
- Introduce a new field, `dlp_wait_time`, in the response of GET `/file/{data_id}` API requested from MetaDefender Cluster API Gateway.
- Include `username` field in the response of GET `/file/{data_id}`, GET `/file/batch/{batch_id}` and GET `/hash/{md5|sha1|sha256|sha512}`.

---

**Further Enhancements**

- Verify the minimum version requirement when adding a new instance of Redis, RabbitMQ, and PostgreSQL to MetaDefender Cluster Control Center.
- Improve storing scan results from AV engines to MetaDefender Cluster Data Lake.

---

**Security Enhancements**

Upgraded library for vulnerability fixes:

- OpenSSL 3.5.2

**Bug Fixes**

- Fixed the issue that caused occasional service crashes when halted.
- Fixed the issue that made it impossible to close a batch if its name contained special characters.
- Fixed the issue that led to the batch name not appearing in the UI of MD Cluster Control Center.
- Fixed the issue that caused the COO engine to fail or time out during installation.
- Fixed the issue that caused the executive report to eventually miss data.

---

**Known limitations**

MetaDefender Core becomes unlicensed following the MD Cluster Worker upgrade.

- If online activation is used, follow [Online Activation](/docs/mdcluster/installation/md-cluster-online-activation) activate MetaDefender Core again.
- Otherwise, follow [Offline Activation](/docs/mdcluster/installation/md-cluster-offline-activation).

## [Version v2.3.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v230)

Release Date: 28 August 2025

**Offline License Activation**

Offline license activation of MetaDefender Core instances within the cluster is supported for air-gapped environment.

---

**Offline Engine Package Upload**

In offline environment, administrators can manually upload engine packages to MetaDefender Cluster Control Center.

---

**Centralized Online Engine Package Update**

At update time, engine packages are obtained once from the cloud and shared with all MetaDefender Core instances within the cluster to retrieve, install, or update.

---

**System and Instance Activities**

System Activity page allows administrators to track the total processing objects, average CPU usage of the entire system, processed objects and other resources consumed by individual MetaDefender Core instances, all in one place.

---

**High Availability support for** **PostgreSQL Data Lake**

Administrators can add multiple PostgreSQL instances to ensure high availability for Data Lake.

---

**Cancellation of Remote Support Package Gathering**

Administrators have the option to cancel the gathering of Remote Support Package from the MetaDefender Cluster console at any point. The cancellation is carried out at the earliest opportunity.

---

**Support Package Gathering within a specified timeframe**

MetaDefender Cluster enables administrators to define a time period for gathering support packages.

---

**RESTful API**

- Introduce a new API endpoint in MetaDefender Cluster API Gateway to fetch information on the longest expiry active license GET `/admin/license`.
- Introduce a new field, `filetype_wait_time`, in the response of GET `/file/{data_id}` API requested from MetaDefender Cluster API Gateway.

---

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- 7zip 25.01
- Nginx 1.28.0
- PostgreSQL 14.19

**Bug Fixes**

- Fixed an issue that caused the MetaDefender Cluster Control Center to occasionally crash upon stopping.
- Fixed an issue that caused session timeouts to exceed the configured duration.

## [Version v2.2.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v220)

Release Date: 30 July 2025

**Support adding Redis Caching server with username and password**

Administrator can add Redis Caching server including username and password to MetaDefender Cluster.

---

**High Availability support for** **Redis Caching Server, RabbitMQ Message Broker and MetaDefender Cluster File Storage**

Administrators can add multiple instances of Redis, RabbitMQ and MetaDefender Cluster File Storage for High Availability support.

---

**New Dashboard for High Availability support**

A new dashboard is designed to show brief information about critical components of MetaDefender Cluster.

---

**Remote Support Package Gathering**

A feature to collect support packages remotely by the web console of MetaDefender Cluster Control Center.

---

**RESTful API**

- Introduce a new API endpoint in MetaDefender Cluster API Gateway to fetch a list of active MetaDefender Core instances and their details: GET /stat/nodes.
- Introduce a new API endpoint in MetaDefender Cluster API Gateway to fetch a list of active engines and their properties GET /stat/engines.

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- Angular v19
- SQLite 3.47.2

**Bug Fixes**

- Fixed an issue where MetaDefender Cluster API Gateway always responded with HTTP code 500 when clients attempt to call the API GET `/hash/{md5|sha1|sha256|sha512}` with `rule` header.
- Fixed an issue that caused MetaDefender Cluster File Storage to peg at 100% CPU in certain cases.
- Fixed an issue that prevented MetaDefender Cluster components from restarting after an upgrade to the newer version on Windows Server 2025.
- Fixed an issue that prevented MetaDefender Cluster File Storage from upgrading to the newer version on Rocky.

## [Version v2.1.0](/docs/mdcluster/release-notes/mddc-archived-release-notes#version-v210)

Release Date: 03 July 2025

**Update product name**

Introduce **MetaDefender Cluster** as the new product name.

---

**RESTful API**

- Support `include-inprogress` header in GET `/hash/{md5|sha1|sha256|sha512}` to fetch the scan status of the latest request by hash, including incomplete ones.
- Support `Content-Encoding` header in POST `/file`.

**Further Enhancements**

- Turn `storage.path` key in the ignition file for MetaDefender Cluster File Storage into an optional setting.
- Correct the returned HTTP code when the user signs in to or signs out from MetaDefender Cluster Control Center with the wrong information.
- Correct the returned HTTP code when POST `/file` is called with wrong API key.

**Security Enhancements**

Upgraded libraries for vulnerability fixes:

- PostgreSQL v14.18
- yaml-cpp v0.8.0

**Bug Fixes**

- Fixed an issue where MetaDefender Cluster Control Center can't show scan results of in-progress files on the web console.
- Fixed an issue that caused MetaDefender Cluster API Gateway and MetaDefender Core to be impossible to deploy after a deployment failure.
- Fixed an issue that caused MetaDefender Cluster File Storage to crash while downloading file when DEBUG log is enabled.
- Fixed an issue that caused MetaDefender Cluster File Storage impossible to do data retention with the setting.
- Fixed an issue that caused the MetaDefender Cluster Worker to fail to upgrade due to an engine crash while MetaDefender Core was hosted on the worker.
- Fixed an issue that caused the system administrator to be unable to access the Module page in the MetaDefender Cluster Control Center web console.
