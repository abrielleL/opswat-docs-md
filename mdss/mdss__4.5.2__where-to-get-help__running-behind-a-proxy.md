<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/running-behind-a-proxy -->

# Running behind a proxy

#### Application-level proxy (customer.env)

MDSS services read proxy settings from `/etc/mdss/customer.env` (see [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) ).

```bash
HTTP_PROXY="http://proxy_ip:proxy_port"
HTTPS_PROXY="https://proxy_ip:proxy_port"

NO_PROXY=apigateway,commonservices,core,discoveryalibabacloudservice,discoveryamazonsdkservice,discoveryazureblobservice,discoveryazurefilesservice,discoveryboxservice,discoverygooglecloudservice,discoverymftservice,discoverynfsservice,discoveryonedriveservice,discoveryservice,discoverysftpservice,discoverysmbservice,jobdispatcher,licensingservice,loadbalancerservice,loggingservice,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,remediationsservice-alibabacloud,remediationsservice-amazonsdk,remediationsservice-azureblob,remediationsservice-azurefiles,remediationsservice-box,remediationsservice-googlecloud,remediationsservice-mft,remediationsservice-nfs,remediationsservice-onedrive,remediationsservice-sftp,remediationsservice-smb,scanningservice,sftpservice,smbservice,storagesservice,storagesservice-alibabacloud,storagesservice-amazonsdk,storagesservice-azureblob,storagesservice-azurefiles,storagesservice-box,storagesservice-googlecloud,storagesservice-mft,storagesservice-nfs,storagesservice-onedrive,storagesservice-sftp,storagesservice-smb,identityservice,webclient,workflowmanagerservice
```

```bash
HTTP_PROXY="http://username:password@proxy_ip:proxy_port"
HTTPS_PROXY="http://username:password@proxy_ip:proxy_port"

NO_PROXY=apigateway,commonservices,core,discoveryalibabacloudservice,discoveryamazonsdkservice,discoveryazureblobservice,discoveryazurefilesservice,discoveryboxservice,discoverygooglecloudservice,discoverymftservice,discoverynfsservice,discoveryonedriveservice,discoveryservice,discoverysftpservice,discoverysmbservice,jobdispatcher,licensingservice,loadbalancerservice,loggingservice,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,remediationsservice-alibabacloud,remediationsservice-amazonsdk,remediationsservice-azureblob,remediationsservice-azurefiles,remediationsservice-box,remediationsservice-googlecloud,remediationsservice-mft,remediationsservice-nfs,remediationsservice-onedrive,remediationsservice-sftp,remediationsservice-smb,scanningservice,sftpservice,smbservice,storagesservice,storagesservice-alibabacloud,storagesservice-amazonsdk,storagesservice-azureblob,storagesservice-azurefiles,storagesservice-box,storagesservice-googlecloud,storagesservice-mft,storagesservice-nfs,storagesservice-onedrive,storagesservice-sftp,storagesservice-smb,identityservice,webclient,workflowmanagerservice
```

> **Warning**
>
> The configured scan instance address should also be added to the `no_poxy` list if connecting to it does not require a proxy.

#### Docker daemon proxy (pulling MDSS images)

If a proxy is required to access to docker hub in order to pull MDSS images, then this guide should be followed: [https://docs.docker.com/network/proxy/](https://docs.docker.com/network/proxy/)

Create the drop-in config file or edit it if it already exists:

```bash
sudo mkdir -p /etc/systemd/system/docker.service.d
sudo nano /etc/systemd/system/docker.service.d/http-proxy.conf
```

Set the proxy settings:

```bash
[Service]
Environment="HTTP_PROXY=http://proxy_ip:proxy_port"
Environment="HTTPS_PROXY=http://proxy_ip:proxy_port"
Environment="NO_PROXY=localhost,127.0.0.1"
```

Apply the changes:

```bash
sudo systemctl daemon-reload
sudo systemctl restart docker
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
