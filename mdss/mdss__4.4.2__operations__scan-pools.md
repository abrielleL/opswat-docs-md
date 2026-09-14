<!-- source: https://www.opswat.com/docs/mdss/4.4.2/operations/scan-pools -->

# Scan Pools

MetaDefender Storage Security uses scan pools to group instances of MetaDefender Core or MetaDefender Cloud.

These two types of scan pools can be used to balance the load of scan requests.

MD Core API Endpoints and Permissions

To learn more about the required permissions and the endpoints used by MDSS for MD Core, please read the following KB article: [Which API endpoints from MD Core does MDSS utilize?](/docs/mdss/4.4.2/knowledge-base/what-endpoints-from-mdcore-does-mdss-call)

MD Cloud Private Processing

MD Cloud instances use private processing by default to ensure maximum data privacy and security. Therefore, a non-Community API key must be used when integrating in MDSS. With private processing:

- All submitted files are automatically deleted immediately after analysis completion
- Scan results are only accessible to the original API key owner
