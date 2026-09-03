<!-- source: https://www.opswat.com/docs/mdcluster/configurations/remote-support-package-gathering -->

# Remote Support Package Gathering

The support package contains log files and is essential for OPSWAT to troubleshoot issues. Since version **2.2.0**, it is now possible to gather a support package remotely via the web console of the MetaDefender Cluster Control Center.

Info

Ensure that all MD Cluster services are upgraded to version 2.2.0 or higher to fully support this feature.

### [Remote support package gathering steps:](/docs/mdcluster/configurations/remote-support-package-gathering#remote-support-package-gathering-steps)

1. Go to `Settings` > `Export` .
2. Select which MetaDefender Cluster services need to generate support package, then select `Generate`

Info

Select the MetaDefender Cluster Worker service to generate a support package for its deployed instance as well.

3. Wait for the generation process to complete successfully. Once it is done, the download button will appear, and the support packages will be ready for download.

Info

The size of the support package may vary depending on log size and the number of days for collection. If disk space is insufficient, certain log files may be excluded from the support package.

Warning

All support package files will be downloaded to the MetaDefender Cluster Control Center. Please monitor the disk space on the host running this service when using this functionality, as the size of log files can be very large.

4. Click `Download`

Info

Some services may fail due to connection issues or insufficient disk space. In such cases, only the successfully generated support packages will be available for download. Users can view detailed error information if failures occur.
