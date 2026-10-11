<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-distributed-cluster -->

# Configuring with MetaDefender Distributed Cluster

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Starting from MetaDefender Kiosk 4.7.10, administrators can integrate with the MetaDefender Distributed Cluster (MDDC) (2.3.0 or later) to serve very large deployments while offering improved auto-scaling, high availability and fault tolerant capabilities for MetaDefender Core.

Setup MetaDefender Distributed Cluster

For instruction to setup MetaDefender Distributed Cluster, refer to [MetaDefender Distributed Cluster](https://www.opswat.com/docs/mddistributedcluster)

Limitations on MetaDefender Distributed Cluster 2.3.0

The following features are not supported in MetaDefeder Distributed Cluster 2.3.0

- Hash lookup feature (supported in MDDC 2.4.0)
- Manifest generation from Core (supported in MDDC 2.4.0)
- Kiosk gets stuck at processing when one of the Core workers has no license
- Logs may show message as 'MetaDefender Core' instead of 'MetaDefender Distributed Cluster'

Setting up MetaDefender Distributed Cluster with MetaDefender Kiosk consists of the following steps:

## [Detecting the MetaDefender Distributed Cluster server URL](/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-distributed-cluster#detecting-the-metadefender-distributed-cluster-server-url)

MetaDefender Kiosk muse be able to reach the MDDC server URL

1. Access the MetaDefender Kiosk Management Conosle at `http(s)://<ip or dns>:8009`. You can also access the Kiosk Management Console using Windows **Start** > **OPSWAT** > **MetaDefender Kiosk Management Console**.
2. Click **Configuration** and enter your MetaDefender Distributed Cluster URL e.g `http(s)://<ip or dns>:8899`

## [Authenticating the MDDC connection](/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-distributed-cluster#authenticating-the-mddc-connection)

You must authenticate your connection by obtaining an API key from the MetaDefender Distributed Cluster Management Console

1. Access the MDDC Management Console
2. Select User Management
3. Click the desired user with an Administrator role and copy the contents of the `API key` field. If an API key has not been previously generated click the `Generate` link and make sure to save changes.
4. Return to the MetaDefender Kiosk Management Console and click the `Configuration` tab
5. Paste your MDDC API key value in the `API Key` field

## [Associating workflows in Kiosk to workflows in MDDC](/docs/mdkiosk/v4.8.6/configuration/configuring-with-metadefender-distributed-cluster#associating-workflows-in-kiosk-to-workflows-in-mddc)

Refer to [Selecting a Server to Process Files](/docs/mdkiosk/v4.8.6/operating/selecting-a-server-to-process-files)
