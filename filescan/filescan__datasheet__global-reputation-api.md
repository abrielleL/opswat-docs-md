<!-- source: https://www.opswat.com/docs/filescan/datasheet/global-reputation-api -->

# Global Reputation API

**MetaDefender Aether** (previously known as MetaDefender Sandbox) now provides an API endpoint which can be used as a Single Source of Truth (SSOT,) global reputation lookup. It is a set of convenient API endpoints that can be called as the first point of contact to determine whether or not to do a full scan. The endpoint is extremely fast and will contain verdict information related to SHA256 hashes, domains, URLs or IPs.

Info

Please read the MD Cloud Reputation API integration page to learn how to enable this integration: <https://docs.opswat.com/filescan/integrations/reputation-api-integration>

The hash endpoint accepts an SHA256 hash (or a list of SHA256 hashes in case of bulk lookup) and calculates an overall verdict for the given hash based on 4 information sources:

- **OPSWAT MetaDefender Cloud**: if you provide a MetaDefender Cloud API key in the administrator settings, MetaDefender Aether is capable of checking the given hash for reputation on OPSWAT MetaDefender Cloud. The response, which contains the number of available AV engines and the number of AV engines which detected the file with the given hash as malicious, will be visible on the SSOT endpoint also. The ratio between all and detected AV engines is used to calculate the overall verdict.
- **Fuzzyhash:** for each sample file a fuzzyhash is calculated. If SSOT receives a hash for which Filescan can match a fuzzyhash (from previous reports), it will check if that fuzzyhash belongs to a malicious or suspicious cluster. This is also an input for calculating the overall verdict.
- **Community vote:** for each sample the users can vote on the UI if the sample is malicious or benign. The number of malicious and benign votes are considered during calculating the overall verdict.
- **Previous reports:** if previous scans are available for the given hash, the algorithm uses the verdict of these reports too.

The domain, URL and IP endpoints calculate an overall verdict based on the following information sources:

- **OPSWAT MetaDefender Cloud**: just like for hashes, a MetaDefender Cloud reputation lookup is made to check whether the given domain, URL or IP address is malicious.
- **Community vote:** users can vote for maliciousness
- **Previous reports:** if previous scans are available for the given domain, IP or url, the algorithm uses the verdict of these reports too.

Note: to fine-tune the algorithm please set the reputation values in the Administrator menu under configuration tab, however the default values should be sufficient.

For examples and the API definition, please check the Swagger or the API reference and look for /api/reputation (POST and GET) endpoints.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
