<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/installation/troubleshooting-containers -->

# Troubleshooting Containers

## [Kubernetes](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#kubernetes)

### [How to check the logs with Kubectl](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#how-to-check-the-logs-with-kubectl)

- In case the md-icapsrv pod does not initialize we need to check the pod logs to see why is failing

  1. The worker node running the md-icapsrv pod doesn’t have enough resources allocated for the pod. (Pending state)
  2. Provide the License Key in file values.yml if not provided the health check will fail as the container cannot be activated
  3. Need to set value ACCEPT_EULA is true if the application can not start with reason accept EULA.
  4. If you have enabled TLS to need to uncomment `scheme: HTTPS` in health check. The key of the secret need to mapping with the field .certSecretSubPath and .certKeySecretSubPath

BashCopykubectl logs <pod_name> -n <namespace>
### [Start a Bash session](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#start-a-bash-session)

1. Find the MetaDefenteder ICAP Server pod with the command

cmdCopykubectl get pods -A

→ pod name: `md-icapsrv-77c4654f4b-bkclc`

→ namespace: `default`

2. Start a Bash session

cmdCopycommand:
kubectl exec -n <namespace> -it -c <container name> <pod name> bash
E.g:
kubectl exec -n default -it -c md-icapsrv md-icapsrv-77c4654f4b-bkclc bashInfo

Default container name when you use MetaDefender ICAP Server’s Helm chart is `md-icapsrv`

### [Collect support packages](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#collect-support-packages)

There are two different support packages that can be generated.

1. Support package from local machine
2. Support package with script within the pod

#### [Support package from local machine](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#support-package-from-local-machine)

This is the easiest way to have a first idea of what could be happening in the environment. It will collect

- Logs from running pods
- Logs from previous pods
- Configmap

To run this script from your local machine please see [metadefender-k8s/troubleshooting at main · OPSWAT/metadefender-k8s](https://github.com/OPSWAT/metadefender-k8s/tree/main/troubleshooting)

BashCopy./sp.sh <NAMESPACE>
#### [Support package with script within the pod](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#support-package-with-script-within-the-pod)

After accessing to the bash of the container. To create a package you must start the script found under

cmdCopy${INSTALL_ROOT}/usr/bin/mdicapsrv-collect-support-data.sh

As the script processes the necessary information, the script generates the support package output.

The package file is a tar.gz archive with the following name:

cmdCopymdicapsrv--support-<TIMESTAMP>.tar.gz

Where the timestamp was the date when the package was generated.

Example:

cmdCopymdicapsrv--support-1660647413.tar.gz

The generated package will be placed in the same location as the script that was called.

Warning

If you run container with **read-only file system mode** or **non-root user** make sure you have write permission to the working directory when you execute collect support packages script

## [Copy the support package from the container to outside](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#copy-the-support-package-from-the-container-to-outside)

Use `kubectl cp` [Kubectl Reference Docs (kubernetes.io)](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#cp)

BashCopy# Copy /tmp/foo from a remote pod to /tmp/bar locally
kubectl cp <some-namespace>/<some-pod>:/tmp/foo /tmp/bar

Example:

cmdCopykubectl cp default/md-icapsrv-77c4654f4b-bkclc:/mdicapsrv--support-1660648209.tar.gz /home/icap/mdicapsrv--support-1660648209.tar.gz
## [Docker](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#docker)

### [Collect logs](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#collect-logs)

You can collect the logs of the container running

BashCopydocker logs <container_name>
### [Collect support package](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#collect-support-package)

#### [Start a Bash session](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#start-a-bash-session)

1. Find the CONTAINER ID by command

dockerCopydocker container ls -a

E.g: the container ID = d1769cb64afe

2. Start a Bash session with the command docker exec -it <container id> bash

dockerCopydocker exec -it d1769cb64afe bash
#### [Support package with script within the pod](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#support-package-with-script-within-the-pod)

To create a package you must start the script found under

cmdCopy${INSTALL_ROOT}/usr/bin/mdicapsrv-collect-support-data.sh

As the script processes the necessary information, the script generates the support package output.

The package file is a tar.gz archive with the following name:

cmdCopymdicapsrv--support-<TIMESTAMP>.tar.gz

Where the timestamp was the date when the package was generated.

Example:

cmdCopymdicapsrv--support-1660647413.tar.gz

The generated package will be placed in the same location as the script that was called.

Warning

If you run container with **read-only file system mode** or **non-root user** make sure you have write permission to the working directory when you execute collect support packages script

#### [Copy the support package from the container to outside](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#copy-the-support-package-from-the-container-to-outside)

### [Docker](/docs/mdicap/v5.14.1/installation/troubleshooting-containers#docker)

Use [docker cp | Docker Documentation](https://docs.docker.com/engine/reference/commandline/cp/) `docker cp [OPTIONS] CONTAINER:SRC_PATH DEST_PATH|-`

Example:

cmdCopydocker cp d1769cb64afe:/mdicapsrv--support-1660647413.tar.gz /home/icap
