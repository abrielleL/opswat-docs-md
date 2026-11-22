<!-- source: https://www.opswat.com/docs/mdcluster/operating/operating-export -->

# Generate Support Package

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool

This section will allow the system administrator to export MetaDefender Cluster (MD Cluster) support packages. Go to `Settings` and click `Generate Support Package` to open the `Export Support Package` panel. The support package contains all relevant information to help us diagnose the issue of MetaDefender Cluster.

Warning

MD Cluster Support Package does not include logs from services like Redis, RabbitMQ and PostgreSQL. To obtain the service logs, please click [here](/docs/mdcluster/trouble-shooting/collect-log-support-package#collect-service-logs).

- Simply select the `Service Type` and `Time Range`, check the MD Cluster components to include (all are selected by default) and click the `Generate` button. A new ID and notification will be shown in the `Support Package Details.`

- Once the support package generation is finished, simply select `Download` from the `...` menu in the `Actions` column in the `Support Package Details.`
