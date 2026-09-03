<!-- source: https://www.opswat.com/docs/mdcloud/operation/api-security-faq -->

# API Security FAQ

- Confidentiality
- Availability

  - Availability SLA
  - Redundancy
  - BCP (Business Continuity Plan) / DRP (Disaster Recovery Plan)
  - Alerting
  - Service locations
- OPSWAT Compliance and Certifications

  - ISO 27001 Certification
  - SOC2 Certification
  - Independent penetration testing
  - Secure SDLC at OPSWAT

## [Confidentiality](/docs/mdcloud/operation/api-security-faq#confidentiality)

- Questions about the data OPSWAT collects, how OPSWAT uses the customer’s data, sharing the customer’s data with Service Providers, and Data Retention Policies are included in the OPSWAT [Privacy Policy](https://docs.opswat.com/policies/privacy-policy/metadefender-cloud-privacy-policy). OPSWAT uses HTTPS for communication and AES 256 for storage.
- When uploading files in private mode and requesting to run Deep CDR, the file’s sanitized version will be available to download for 24 hours. Once the file is expired to download, the sanitized version of the file is deleted permanently. Sanitized versions can be expired and deleted before 24-hour expiration by calling the [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Delete the sanitized version of the file).
- For all the paid customers, MetaDefender Cloud provides the ability to scan files privately. This private scanning feature is available via all interfaces, including the [MetaDefender Cloud APIs](https://www.opswat.com/docs/mdcloud/integrations/public-apis). All files scanned in private mode will be permanently removed as soon as the analysis is completed, except metadata such as scan results will remain available in the MetaDefender Cloud. Data in transfer

  - REST API use HTTPS with TLS 1.2.
  - Enterprise licensing customers can utilize Mutual TLS (mTLS) Authentication for communication.
  - Any internal service communicates with other services through internal (not exposed to the Internet) load balancers.
- The organization’s administrator can set the policy to enforce a private scanning option for all usages from the organization for the enterprise licensing customers.
- Data in use

  - Access to data is restricted to limited authorized personnel (CloudOps).
- Access control

  - OPSWAT leverages multi-factor authentication (MFA) with the least privilege principle.
- Access log

  - The access log is pseudonymized before it is stored with AES 256 encryption on the data warehouse or data lake.

## [Availability](/docs/mdcloud/operation/api-security-faq#availability)

### [Availability SLA](/docs/mdcloud/operation/api-security-faq#availability-sla)

**Standard and Professional licensing plan**

- 99.5% for Standard and Professional licensing plans. Real-time availability is published at [trust.opswat.com](http://trust.opswat.com/), and anyone can subscribe for any production issue.

**Enterprise licensing plan**

- 99.9% for Enterprise licensing plan. Real-time availability is published at [trust.opswat.com](http://trust.opswat.com/), and anyone can subscribe for any production issue.

### [Response Time SLA](/docs/mdcloud/operation/api-security-faq#response-time-sla)

**Standard licensing plan**

- 8 seconds for scanning and CDR (p50). P50 in this case means that the median (or middle value) of all scan times across a given month falls at or under 8 seconds.
- 500 milliseconds for API calls (p50). P50 in this case means that the median (or middle value) of all API calls across a given month falls at or under 500 milliseconds.

**Professional licensing plan**

- 8 seconds for scanning and CDR (p75). P75 in this case means that 75% of all scan times across a given month falls at or under 8 seconds.
- 500 milliseconds for API calls (p75). P75 in this case means that 75% of all API calls across a given month falls at or under 500 milliseconds.

**Enterprise licensing plan**

- 8 seconds for scanning and CDR (p90). P90 in this case means that 90% of all scan times across a given month fall at or under 8 seconds.
- 500 milliseconds for API calls (p90). P90 in this case means that 90% of all API calls across a given month fall at or under 500 milliseconds.

### [Redundancy](/docs/mdcloud/operation/api-security-faq#redundancy)

- All systems accepting user traffic are set up to use auto-scaling. More resources are provisioned as traffic increases (scale-out).

### [BCP (Business Continuity Plan) / DRP (Disaster Recovery Plan)](/docs/mdcloud/operation/api-security-faq#bcp-business-continuity-plan--drp-disaster-recovery-plan)

- The service uses High Availability infrastructure with backup.
- OPSWAT provides the following recoverability SLAs depending on the Customer licensing plan:

  - For the Commercial licensing plan, OPSWAT provides an RTO of 24 hours.
  - For Enterprise licensing plan, OPSWAT provides an RTO of 4 hours.
  - In a situation when disaster recovery is required, new infrastructure will be created in different regions with automated deployment. OPSWAT does not have hot backup servers but cold backups.
- Data is backed up daily as snapshots and backups are kept for one week.
- DR testing and tests reports:

  - Testing is performed once a year.
  - Tests reports are available by request.

### [Alerting](/docs/mdcloud/operation/api-security-faq#alerting)

- Does the system send alerts when it isn't functioning or is under stress?

  - Refer to [Incident Reporting on MetaDefender Cloud](/docs/mdcloud/legal/incident-reporting-on-metadefender-cloud)
  - OPSWAT provides a service on [trust.opswat.com](http://trust.opswat.com/) allowing any customer to view outages.

### [Service Locations](/docs/mdcloud/operation/api-security-faq#service-locations)

- Where is the system located? (Country(s) - Cloud / Hybrid / On-Premise)

  - Cloud: Customers can select between Europe (Germany), the USA (North America), Canada (Montreal), Australia (Sydney). OPSWAT values the experience and privacy of our users. Our service is provided by servers located in the following [locations](/docs/mdcloud/compliance/locations). Please consult with the product team if you would like to see a service closer to the customer’s region.
  - Response time: OPSWAT is continuously monitoring the response time for its services. You can find the average scan times on [Metadefender Cloud Statistics](https://www.opswat.com/docs/mdcloud/operation/average-scan-times)

## [OPSWAT Compliance and Certifications](/docs/mdcloud/operation/api-security-faq#opswat-compliance-and-certifications)

For the latest and complete list of OPSWAT Compliance and Certifications, visit:

<https://www.opswat.com/company/compliance-and-certifications>

### [ISO 27001 Certification](/docs/mdcloud/operation/api-security-faq#iso-27001-certification)

OPSWAT has achieved ISO/IEC 27001:2022 certification. An independent examination of the OPSWAT Information Security Management System (ISMS) and OPSWAT MetaDefender and MetaAccess services by Schellman & Company, LLC confirmed our commitment to security and regulatory compliance as part of the certification evaluation.

### [SOC2 Certification](/docs/mdcloud/operation/api-security-faq#soc2-certification)

SOC for Service Organizations reports is designed to help service organizations that provide services to other entities, build trust and confidence in the service performed and controls related to the services through a report by an independent CPA. SOC 2 controls are evaluated at a Service Organization that is relevant to Security, Availability, Processing Integrity, Confidentiality or Privacy related to systems the service organization uses to process users’ data and the confidentiality and privacy of the information processed by these systems.

- OPSWAT can share SOC2 Type 2 report by request

### [Independent Penetration Testing](/docs/mdcloud/operation/api-security-faq#independent-penetration-testing)

- OPSWAT is performing various external independent penetration testing at least once a year or whenever significant changes are made.

### [Secure SDLC at OPSWAT](/docs/mdcloud/operation/api-security-faq#secure-sdlc-at-opswat)

OPSWAT follows the Agile Software Development Lifecycle. On top of the agile process, we have added OWASP [SAMM](http://owasp.org/www-project-samm/)  as the framework for the Secure Software Development Life Cycle and OWASP [ASVS](http://owasp.org/www-project-samm/) as the framework for Application Security and Verification.

Refer to [Secure SDLC at OPSWAT](https://www.opswat.com/blog/secure-sdlc-at-opswat) for more information.
