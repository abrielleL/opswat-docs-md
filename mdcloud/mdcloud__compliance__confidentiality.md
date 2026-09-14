<!-- source: https://www.opswat.com/docs/mdcloud/compliance/confidentiality -->

# Confidentiality

## [Data Confidentiality](/docs/mdcloud/compliance/confidentiality#data-confidentiality)

Questions about the data OPSWAT collects, how OPSWAT uses the customer’s data, sharing the customer’s data with Service Providers, and Data Retention Policies are included in the OPSWAT [Privacy Policy](https://docs.opswat.com/policies/privacy-policy/metadefender-cloud-privacy-policy). OPSWAT uses HTTPS for communication and AES 256 for storage.

When uploading files in private mode and requesting to run Deep CDR, the file’s sanitized version will be available to download for 24 hours. After that 24 hour window, the file is expired to download and the sanitized version of the file is deleted permanently. Sanitized versions can be expired and deleted before 24-hour expiration by calling the [Metadefender Cloud API](https://docs.opswat.com/mdcloud/v4/metadefender-cloud-api-v4/ref#Delete%20the%20sanitized%20version%20of%20the%20file).

For paid customers, MetaDefender Cloud provides the ability to scan files privately. This private scanning feature is available via all interfaces, including the [MetaDefender Cloud APIs](https://docs.opswat.com/operation/analyzing-binaries-with-metadefender-cloud/private-scanning-with-metadefender-cloud-apis). All files scanned in private mode will be permanently removed as soon as the analysis is completed, except metadata such as scan results will remain available in the MetaDefender Cloud.

If you are using the organization feature for MetaDefender Cloud, your organization’s administrator can set a policy to enforce the private scanning option for all usages from the organization for the enterprise licensing customers.

## [Data in Transfer](/docs/mdcloud/compliance/confidentiality#data-in-transfer)

- REST API uses HTTPS with TLS 1.2
- Customers with enterprise level licensing can utilize Mutual TLS (mTLS) Authentication for communication
- Any internal service communicates with other services through internal (not exposed to the Internet) load balancers

## [Data in Use](/docs/mdcloud/compliance/confidentiality#data-in-use)

- Access to data is restricted to limited authorized personnel (CloudOps)

## [Access Control](/docs/mdcloud/compliance/confidentiality#access-control)

- Opswat leverages multi-factor authentication (MFA) while applying the principle of least privilege (i.e. users are given the least amount of access required to adequately perform the duties of their role)

## [Access Log](/docs/mdcloud/compliance/confidentiality#access-log)

- The access log is pseudonymized before it is stored with AES 256 encryption on the data warehouse or data lake (*Pseudonymization is a data management and de-identification procedure by which personally identifiable information fields within a data record are replaced by one or more artificial identifiers, or pseudonyms)*
