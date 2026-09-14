<!-- source: https://www.opswat.com/docs/mdss/4.4.2/where-to-get-help/running-behind-a-proxy -->

# Running behind a proxy

#### [Application-level proxy (customer.env)](/docs/mdss/4.4.2/where-to-get-help/running-behind-a-proxy#application-level-proxy-customerenv)

MDSS services read proxy settings from `/etc/mdss/customer.env` (see [Custom configuration](/docs/mdss/4.4.2/configuration/custom-configuration) ).

customer.env without credentialsCopyHTTP_PROXY="http://proxy_ip:proxy_port"
HTTPS_PROXY="https://proxy_ip:proxy_port"
NO_PROXY=apigateway,commonservices,core,discoveryalibabacloudservice,discoveryamazonsdkservice,discoveryazureblobservice,discoveryazurefilesservice,discoveryboxservice,discoverygooglecloudservice,discoverymftservice,discoverynfsservice,discoveryonedriveservice,discoveryservice,discoverysftpservice,discoverysmbservice,jobdispatcher,licensingservice,loadbalancerservice,loggingservice,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,remediationsservice-alibabacloud,remediationsservice-amazonsdk,remediationsservice-azureblob,remediationsservice-azurefiles,remediationsservice-box,remediationsservice-googlecloud,remediationsservice-mft,remediationsservice-nfs,remediationsservice-onedrive,remediationsservice-sftp,remediationsservice-smb,scanningservice,sftpservice,smbservice,storagesservice,storagesservice-alibabacloud,storagesservice-amazonsdk,storagesservice-azureblob,storagesservice-azurefiles,storagesservice-box,storagesservice-googlecloud,storagesservice-mft,storagesservice-nfs,storagesservice-onedrive,storagesservice-sftp,storagesservice-smb,identityservice,webclient,workflowmanagerservicecustomer.env with credentialsCopyHTTP_PROXY="http://username:password@proxy_ip:proxy_port"
HTTPS_PROXY="http://username:password@proxy_ip:proxy_port"
NO_PROXY=apigateway,commonservices,core,discoveryalibabacloudservice,discoveryamazonsdkservice,discoveryazureblobservice,discoveryazurefilesservice,discoveryboxservice,discoverygooglecloudservice,discoverymftservice,discoverynfsservice,discoveryonedriveservice,discoveryservice,discoverysftpservice,discoverysmbservice,jobdispatcher,licensingservice,loadbalancerservice,loggingservice,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,remediationsservice-alibabacloud,remediationsservice-amazonsdk,remediationsservice-azureblob,remediationsservice-azurefiles,remediationsservice-box,remediationsservice-googlecloud,remediationsservice-mft,remediationsservice-nfs,remediationsservice-onedrive,remediationsservice-sftp,remediationsservice-smb,scanningservice,sftpservice,smbservice,storagesservice,storagesservice-alibabacloud,storagesservice-amazonsdk,storagesservice-azureblob,storagesservice-azurefiles,storagesservice-box,storagesservice-googlecloud,storagesservice-mft,storagesservice-nfs,storagesservice-onedrive,storagesservice-sftp,storagesservice-smb,identityservice,webclient,workflowmanagerserviceWarning

The configured scan instance address should also be added to the `no_poxy` list if connecting to it does not require a proxy.

#### [Docker daemon proxy (pulling MDSS images)](/docs/mdss/4.4.2/where-to-get-help/running-behind-a-proxy#docker-daemon-proxy-pulling-mdss-images)

If a proxy is required to access to docker hub in order to pull MDSS images, then this guide should be followed: <https://docs.docker.com/network/proxy/>

Create the drop-in config file or edit it if it already exists:

BashCopysudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf

Set the proxy settings:

docker serviceCopy[Service]
Environment="HTTP_PROXY=http://proxy_ip:proxy_port"
Environment="HTTPS_PROXY=http://proxy_ip:proxy_port"
Environment="NO_PROXY=localhost,127.0.0.1"

Apply the changes:

BashCopysudo systemctl daemon-reload
sudo systemctl restart docker
