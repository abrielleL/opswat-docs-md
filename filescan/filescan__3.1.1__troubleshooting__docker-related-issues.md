<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/docker-related-issues -->

# Docker-related issues

Versions prior to 1.9.1 are not suitable for a clean installation due to breaking changes introduced in Docker 25. Please **use version 1.9.2 or later** for clean installations!

If you run `bootstrap.sh` to perform a clean installation of Sandbox 1.9.1 (or earlier), then the following `invalid network config` issue will occur due to a breaking change in Docker 25:

Error response from daemon: network no-internet not found
Installing no-internet network in order to isolate powershell container ...
Error response from daemon: invalid network config:
invalid subnet 172.18.0.1/24: it should be 172.18.0.0/24

In this case, you can modify the subnet address in `sandbox-installer/common.sh` to allow the installation to complete.

Please replace this line:

BashCopyecho "Installing no-internet network in order to isolate powershell container ..." && docker network create --internal --subnet 172.18.0.1/24 no-internet && echo "Successfully created docker subnets" || {

with the following:

BashCopyecho "Installing no-internet network in order to isolate powershell container ..." && docker network create --internal --subnet 172.18.0.0/24 no-internet && echo "Successfully created docker subnets" || {

**After completing the installation**, it is strongly recommended to **downgrade all Docker packages**, because Docker 25 breaks communications between certain components of the Sandbox system:

BashCopyDOCKER_CE_VERSION=5:24.0.7-1~ubuntu.20.04~focal
DOCKER_COMPOSE_VERSION=2.21.0-1~ubuntu.20.04~focal
DOCKER_BUILDX_VERSION=0.11.2-1~ubuntu.20.04~focal
CONTAINERD_VERSION=1.6.27-1
sudo apt-get -fy --allow-downgrades install docker-ce=$DOCKER_CE_VERSION \
docker-ce-cli=$DOCKER_CE_VERSION containerd.io=$CONTAINERD_VERSION \
docker-buildx-plugin=$DOCKER_BUILDX_VERSION docker-compose-plugin=$DOCKER_COMPOSE_VERSION

If you encounter the following error when running `shutdown_webservice.sh`, please also downgrade the Docker packages using the commands above (this is a bug in docker compose version 2.24.1 that might be fixed in future versions: <https://github.com/docker/compose/issues/11371>)

err: validating /srv/backend/docker-compose.community.yml: services.reverse_proxy.volumes array items[1,8] must be unique
2024/01/24 11:17:31 Process exited with status 15

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
