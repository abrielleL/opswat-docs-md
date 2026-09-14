<!-- source: https://www.opswat.com/docs/mdmft/v3.11.4/high-availability/faq -->

# FAQ

Summarize Page    Connect to Cursor Connect to VS Code
## [Is the MetaDefender® MFT HA cluster active-active or active-passive?](/docs/mdmft/v3.11.4/high-availability/faq#is-the-product_name_short-ha-cluster-active-active-or-active-passive)

The MFT HA cluster operates in an **active-passive configuration**.

At any given time:

- Only **one MFT node is active** and processing user traffic.
- The other node remains in **passive mode**.

## [How is the HA Controller itself highly available?](/docs/mdmft/v3.11.4/high-availability/faq#how-is-the-ha-controller-itself-highly-available)

The MetaDefender MFT High Availability Controller™ achieves high availability by running three controller instances in a cluster and using the [Raft](https://raft.github.io/) consensus algorithm for leader election and state replication.

You can find more information [here](/docs/mdmft/v3.11.4/high-availability/redundant-ha-controllers).

## [Which storage types are supported in an HA deployment?](/docs/mdmft/v3.11.4/high-availability/faq#which-storage-types-are-supported-in-an-ha-deployment)

In an active-passive HA deployment, MFT requires shared storage that is accessible by both nodes. For more information see [supported storages](/docs/mdmft/v3.11.4/high-availability/requirements#file-storage).

## [How are storage and database high availability handled in an MFT HA deployment?](/docs/mdmft/v3.11.4/high-availability/faq#how-are-storage-and-database-high-availability-handled-in-an-mft-ha-deployment)

The MetaDefender® MFT HA solution provides high availability for the application layer — specifically the MetaDefender® MFT nodes and the MetaDefender MFT HA Controller™.

For database and shared storage availability, we recommend using well-established HA technologies so those components are resilient too:

- For the database a common solution is SQL Server cluster
- For shared storage, use the appropriate HA solution for your chosen backend

## [Can MetaDefender® MFT load balance across multiple MetaDefender Core™ instances?](/docs/mdmft/v3.11.4/high-availability/faq#can-product_name_short-load-balance-across-multiple-core_product_name-instances)

Yes. MetaDefender® MFT supports connecting to **multiple MetaDefender Core™ servers** and distributing file scanning requests across them for both load balancing and resilience.

You can find more information [here](/docs/mdmft/v3.11.4/integrations/metadefender-core-integration#load-balancing-and-high-availability).

## [When integrating with an MFT HA cluster from another application which address should I use?](/docs/mdmft/v3.11.4/high-availability/faq#when-integrating-with-an-mft-ha-cluster-from-another-application-which-address-should-i-use)

You should always configure your external systems (such as applications that upload or retrieve files, eg.: MD Kiosk) to use the load balancer’s address, not the individual active or passive MetaDefender® MFT node addresses.

Info

If you are using a single HA Controller without load balancer then use the address of the single Controller
