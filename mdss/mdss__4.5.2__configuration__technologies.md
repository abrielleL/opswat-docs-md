<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/technologies -->

# Technologies

MDSS monitors the status of the following technologies from MetaDefender  Core:

- Data Loss Prevention
- Deep CDR
- Sandbox
- Metascan

These monitoring is done every 5 minutes to see what changes are done on MetaDefender  Core for these technologies. A manual refresh is available as well to have this check done on demand

This is not available on MetaDefender Cloud

> **Technology Status**
>
> There are three statuses for the technologies:
>
> - **Enabled**
>   - A valid ApiKey was provided for the scan pool and the technology is **available** in the MetaDefender Core instance.
> - **Disabled**
>   - A valid ApiKey was provided for the scan pool and the technology is **unavailable** in the MetaDefender Core instance.
>   - This will prevent allowing to set up actions that are not available in the MetaDefender Core instance.
> - **Unknown**
>   - No ApiKey was provided for the scan pool. The status of the technology from MetaDefender Core instance is unknown.

![](https://uploads.developerhub.io/prod/k8zL/qzw9wf76uzkbyh7jyevtnvw0nba2hw2dqu8q1kg2ofjowt8pp37qur75f9f9pvd8.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
