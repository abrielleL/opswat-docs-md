<!-- source: https://www.opswat.com/docs/mdss/4.6.0/where-to-get-help/running-behind-a-proxy -->

# Running behind a proxy

#### Application-level proxy (customer.env)

MDSS services read proxy settings from `/etc/mdss/customer.env` (see [Custom configuration](https://www.opswat.com/docs/mdss/configuration/custom-configuration) ).

`NO_PROXY` must list every hostname the MDSS containers reach directly on the Docker network, so that service-to-service traffic is not sent through the proxy. The list below covers both deployment modes: the bundled platform container (`md-platform`, the default) and the individual-services deployment (`COMMON_SERVICES_ENABLED=no`). Entries for services that are not running in your deployment are harmless.

```bash
HTTP_PROXY="http://proxy_ip:proxy_port"
HTTPS_PROXY="https://proxy_ip:proxy_port"

NO_PROXY=localhost,127.0.0.1,apigateway,mdcs_apigateway,core,discoveryservice,identityservice,jobdispatcher,licensingservice,loggingservice,md-platform,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,scanningservice,smbservice,storagesservice,webclient,workflowmanagerservice
```

```bash
HTTP_PROXY="http://username:password@proxy_ip:proxy_port"
HTTPS_PROXY="http://username:password@proxy_ip:proxy_port"

NO_PROXY=localhost,127.0.0.1,apigateway,mdcs_apigateway,core,discoveryservice,identityservice,jobdispatcher,licensingservice,loggingservice,md-platform,mongodb,mongomigrations,nfsservice,node,notificationservice,pgmigrations,postgres,rabbitmq,redis,remediationsservice,scanningservice,smbservice,storagesservice,webclient,workflowmanagerservice
```

What the entries are:

| Entry | Deployment | Purpose |
| ---- | ---- | ---- |
| `md-platform` | Bundled (default) | The single container that hosts Identity, Licensing, Job Dispatcher, Logging, Scanning, Notification, Discovery, Remediations, Storages and Workflow Manager |
| `discoveryservice`, `identityservice`, `jobdispatcher`, `licensingservice`, `loggingservice`, `notificationservice`, `remediationsservice`, `scanningservice`, `storagesservice`, `workflowmanagerservice` | Individual services (`COMMON_SERVICES_ENABLED=no`) | The same services, one container each |
| `apigateway`, `mdcs_apigateway`, `webclient`, `pgmigrations`, `mongomigrations` | Both | API Gateway, web client and the database migration jobs |
| `postgres`, `rabbitmq`, `redis`, `mongodb` | Both | Infrastructure. Replace with your own hostnames when using external PostgreSQL, RabbitMQ or Redis, if they are reachable without a proxy |
| `nfsservice`, `smbservice` | Both, when the NFS or SMB module is enabled | The NFS and SMB protocol sidecars. All other storage types run in-process and need no extra entry |
| `core`, `node` | Both, when MetaDefender Core is deployed alongside MDSS | The bundled MetaDefender Core instance |

> **Warning**
>
> The configured scan instance address should also be added to the `NO_PROXY` list if connecting to it does not require a proxy.

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
