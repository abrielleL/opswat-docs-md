<!-- source: https://www.opswat.com/docs/mdss/4.5.2/operations/scan-pools -->

# Scan Pools

MetaDefender Storage Security uses scan pools to group instances of MetaDefender Core or MetaDefender Cloud.

![](https://uploads.developerhub.io/prod/k8zL/39lsw6ek3tpb02q732vnw4zpkddq3t04f8cltj501br11qd5fjmjnozhr7njgv08.png)

These two types of scan pools can be used to balance the load of scan requests.

> **MD Core API Endpoints and Permissions**
>
> To learn more about the required permissions and the endpoints used by MDSS for MD Core, please read the following KB article: [Which API endpoints from MD Core does MDSS utilize?](https://www.opswat.com/docs/mdss/knowledge-base/what-endpoints-from-mdcore-does-mdss-call)

> **MD Cloud Private Processing**
>
> MD Cloud instances use private processing by default to ensure maximum data privacy and security. Therefore, a non-Community API key must be used when integrating in MDSS. With private processing:
>
> - All submitted files are automatically deleted immediately after analysis completion
> - Scan results are only accessible to the original API key owner

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
