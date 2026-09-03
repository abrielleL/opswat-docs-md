<!-- source: https://www.opswat.com/docs/mdicap/troubleshooting/could-not-create-temporary-directory -->

# Could not create temporary directory

MetaDefender ICAP Server requires temporary directories and files for its operation. If the temporary directory can not be created then the ICAP Server will fail to start with Could not create temporary directory message in the logs.

Example log message on CentOS 7:

[ERROR ] 2017.04.20 05:58:12.731: (common.base) Error in Service, shutdown.., error='Could not create temporary directory: /home/mdicapsrv/temp' [msgid: 8]

Consider the following:

1. Proper access rights are configured on the temporary directory root (see the tempdirectory entry in [3.1.2 MetaDefender ICAP Server configuration file](/docs/mdicap/configuration/configuration-file))
2. There is appropriate amount of free disk space for temporary files on the partition where temporary directory root is configured to

   1. In case of abnormal termination of ICAP Server (crash, power supply problems etc.) there is a chance that temporary files remain under the temporary directory root.

Note

These remaining temporary files require manual cleanup.
