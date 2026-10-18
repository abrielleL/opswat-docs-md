<!-- source: https://www.opswat.com/docs/mdss/4.6.0/getting-started/advanced-deployment-with-managed-services -->

# Advanced Deployment with Managed Services

This setup uses **multiple** MetaDefender Storage Security (MDSS) instances and leverages your cloud provider's managed services for the database, cache, and message broker.  It's designed for high throughput and simplifies management.

![](https://uploads.developerhub.io/prod/k8zL/rzwddonrjlcj6owhkmkstxgvrkdkmwpopskugnc2k9j4etyt4tzb3e67nwy7i09d.jpg)

Imagine having a team of experts (your cloud provider) handle the backend infrastructure, allowing you to focus on scaling and managing your MDSS instances. This setup is powerful and efficient for high-volume workloads.

#### Suitable For

- Organizations processing a lot of files.
- Cloud-Centric Businesses who already leveraging cloud infrastructure.

#### Why It's Powerful

- Multiple MDSS instances handle large workloads efficiently.
- Your cloud provider handles the underlying infrastructure (database, etc.).
- Ideal if you're already using cloud services.
- Get monitoring, reporting, and proactive support from your cloud provider.

#### Example (AWS)

- Database: use Amazon RDS
- Cache: use Amazon ElastiCache
- Message Broker: use Amazon MQ

Adaptable to Azure & Google Cloud: You can use similar services from those providers. For more information on integrating with various cloud providers, please follow this page: [CSP Deployment Overview](https://www.opswat.com/docs/mdss/installation/csp-deployment-overview).

#### Key Benefits

- You manage the MDSS instances, not the database, cache, etc.
- Cloud providers ensure redundancy and availability.
- Tested to handle 100,000 files/hour (with 2+ MDSS and 4+ MDSS Core instances).

**Important Note:** Cloud managed services have associated costs.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
