<!-- source: https://www.opswat.com/docs/myop/configuration/opensearch-integration -->

# OpenSearch Integration

For MetaDefender Core and MetaDefender ICAP' [Scan Reports](https://www.opswat.com/docs/product-management/configuration/scan-reports) feature, My OPSWAT On-premises provides an optional integration feature with an external OpenSearch server for optimized storage and query performance.

To set up OpenSearch integration:

1. Set up an external OpenSearch server. Please refer to the [official OpenSearch documentation](https://docs.opensearch.org/docs/latest/install-and-configure/install-opensearch/index/).
2. Log into the virtual appliance's CLI terminal using the Local User credentials configured during the [setup wizard](/docs/myop/deployment/deployment).
3. Run **sudo /os/prod-scripts/cent-ocm-service.sh stop** to stop My OPSWAT service.
4. Run **sudo /os/prod-scripts/cent-update-docker-profile.sh opensearch** to enable OpenSearch integration mode.
5. Run **vim /home/<user>/bin/opensearch-external.properties** to edit the OpenSearch configuration. The following settings are available by default

   - **OPENSEARCH_ADDRESSES=**[**https://opensearch:9200**](https://opensearch:9200)

     - The address(es) of the external OpenSearch server/cluster.
   - **OPENSEARCH_USERNAME=admin**

     - The username used to access the OpenSearch server. Please note that this username should have administrator privilege.
   - **OPENSEARCH_PASSWORD=placeholder**

     - The password used to access the OpenSearch server.
6. (Optional) Test connection to the OpenSearch server. You can use the built-in **curl** command to test connection to the OpenSearch server.

   - For example, **curl -X GET** [**https://opensearchserver.local:9200**](https://opensearchserver.local:9200) **-u 'admin:<custom-admin-password>' --insecure.**
7. Run **sudo /os/prod-scripts/cent-opensearch-apply.sh** to apply the OpenSearch configuration.
8. Run **sudo /os/prod-scripts/cent-ocm-service.sh start** to start My OPSWAT service.
