<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/configuration-on-k8s -->

# Configuration on K8S

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### [Storage and Database](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#storage-and-database)

MetaDefender ICAP Server container is stateless and do not require persistent storage. However in case it is needed in any scenario here is how you can configure it

YamlCopyextra_storage_configs: # Example for creating PVC for ICAP container. Use extraVolumeMounts and extraVolumes in icap container definition together with this PVC
extra_pvc:
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: icap-disk-pvc
spec:
accessModes:
- ReadWriteMany
resources:
requests:
storage: 5Gi
storageClassName: azurefile
icap_container_persistent: false # To enable for mounting icap path /opt/mdicapsrv/icap_data/var/lib/mdicapsrv using below storage_configs pvc
icap_components:
md_icapsrv:
extraVolumeMounts:
- mountPath: <path_to_mount> # for icap migration from sqlite to postgresql needed to mount -> "/opt/mdicapsrv/icap_data/var/lib/mdicapsrv". From version 5.2.0
subPath: md_icapsrv # subpath with the mounted point
name: icap-disk-pvc # name for the mounting point
extraVolumes:
- name: icap-disk-pvc
persistentVolumeClaim:
claimName: icap-disk-pvc

Also, if deploying the PostgreSQL database within the cluster, it is recommended to use persistent storage managed by your cloud provider.

YamlCopydb_user: postgres # PostgreSQL database username
db_password: postgres # PostgreSQL database password, if not set it will be randomly generated
# Support customize the database name. Default is `metadefender_icapsrv`
db_name: metadefender_icapsrv
postgres_mdicapsrv:
enabled: true
name: postgres-mdicapsrv
image: postgres:16.6
env:
- name: POSTGRES_PASSWORD
valueFrom:
secretKeyRef:
name: mdicapsrv-postgres-cred
key: password
- name: POSTGRES_USER
valueFrom:
secretKeyRef:
name: mdicapsrv-postgres-cred
key: user
ports:
rest: 5432
service_type: ClusterIP
# Example using a PVC with dynamic provisioning from an existing storage class for postgres_mdicapsrv container
storage_configs:
enabled: true
accessModes:
- ReadWriteOnce
resources:
requests:
storage: 100Gi
storageClassName: "default" # to change to you existing storage class allocated by your CSP

An remote database can be configured using the following values:

YamlCopyicap_components:
md_icapsrv:
database:
db_mode: "4" # Database mode
db_type: remote # Database type
db_host: postgres-mdicapsrv # Hostname / entrypoint of the database, this value should be changed any if using an external database service
db_port: "5432" # Port for the PostgreSQL Database

When using an external database not deployed via the MDSS chart, the postgres_mdicapsrv:

value must be set to `false` to prevent the chart from deploying an additional database.

YamlCopypostgres_mdicapsrv:
enabled: true
### [Resource Definition](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#resource-definition)

To indicate the resources to allocate to the MetaDefender ICAP container. Limits are optional.

YamlCopyicap_components:
md_icapsrv:
resources:
requests:
memory: "2Gi" # Minimum reserved memory
cpu: "2.0" # Minimum reserved cpu
#limits:
# memory: "4Gi" # Maximum memory limit
# cpu: "4.0" # Maximum cpu limit
### [Exposing MetaDefender ICAP Server](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#exposing-metadefender-icap-server)

#### [Service Configuration](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#service-configuration)

#### [Ingress Configuration](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#ingress-configuration)

### [Proxy configuration](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#proxy-configuration)

MetaDefender ICAP Server container needs to access to internet for activating the application. In case of needed to use a proxy this is the way to configure it

YamlCopyproxy:
enabled: true
http_proxy: ""
https_proxy: ""
no_proxy: localhost
### [Security Context](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#security-context)

To indicate different security context to adapt the container to the environment security policies

YamlCopysecurityContext:
runAsUser: 1000
runAsGroup: 1000
runAsNonRoot: true
allowPrivilegeEscalation: false
### [Syslog configuration](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#syslog-configuration)

MetaDefender ICAP Server support to send the syslog to a server. This is the way to configure it for the application

- **ICAP it is using ICAP_CONF_JSON environment variable (This example uses Elastic)**

  - **Example: ICAP_CONF_JSON: '{"logger/cef": "true","logger/syslog": "tcp://eck-stack-eck-logstash-ls-tcp.elastic-system:5088","logger/syslog_level": "info"}'**

### [Custom service account](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#custom-service-account)

YamlCopyicap_components:
md_icapsrv:
service_account_name: mdicapsrv-service-account
### [Non-root access on Kubernetes](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#non-root-access-on-kubernetes)

- Modify UID:GID to run as non-root
- create file *override.values.yaml* to override default value

BashCopyACCEPT_EULA: false
mdicapsrv_user: admin # Initial admin user for the MD ICAP Server web interface
mdicapsrv_password: <password> # Initial admin password for the MD ICAP Server web interface, if not set it will be randomly generated
mdicapsrv_license_key: <SET_LICENSE_KEY_HERE> # A valid license key, **this value is mandatory**
icap_components:
md_icapsrv:
securityContext:
runAsUser: 1000 # Specify the UID of the user, id is 1000
runAsGroup: 1000 # Specify the GID of the group, id is 1000
runAsNonRoot: true
allowPrivilegeEscalation: false

- Deploy the helm chart with override values

BashCopyhelm upgrade --install mdicapsrv -n <namespace> -f override.values.yaml .
### [Other Configuration Options](/docs/mdicap/v5.15.0/installation/configuration-on-k8s#other-configuration-options)

Check the table with all the configuration options listed in [this page](https://github.com/OPSWAT/metadefender-k8s/blob/main/helm_charts/mdicapsrv-README.md)
