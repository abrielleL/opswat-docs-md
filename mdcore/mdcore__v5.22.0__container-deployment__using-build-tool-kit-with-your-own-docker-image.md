<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/container-deployment/using-build-tool-kit-with-your-own-docker-image -->

# Using build tool kit with your own docker image

The docker build tool kit could be found on OPSWAT Portal - Products - Utilities

[**https://my.opswat.com/home/metadefender-core**](https://my.opswat.com/home/metadefender-core)

The build tool kit includes following files:

- `Dockerfile` - main script for building docker image.
- `entrypoint.sh` - startup script that runs when the container starts.
- `patch.sh` - utility script for string replacing in file, needed for building docker image.
- `systemctl.py` the replacement for systemctl, needed for non-privileged container.
- `mdcore.sh` - functionalities that `entrypoint.sh` need to start MetaDefender Core service.

To build the image, just run the following command:

build cmdCopydocker build -t <image_name[:tag]> [--build-arg VERSION=<version>] <build-kit_path>

- `<image_name[:tag]>` - name of your built image with optional tag (e.g. `latest` ).
- `--build-arg VERSION=<version>`*-* the desired MetaDefender Core version to be downloaded from OPSWAT. If obmitted then a local installer will be used, installer should be placed in working directory with name is formatted /mdcore/ometascan-*.rpm or .deb (configurable in the Dockerfile).
- `<build-kit_path>` - relative path to your build-kit which contains Dockerfile.

For example:

build cmdCopydocker build -t core:debian --build-arg VERSION=5.13.2 .

In Dockerfile, there are some environment variables that can be modified for various use cases. **You should modify the environment variables before building the MetaDefender Core docker image**.

configCopy# Product version for downloading installer package, ignored if use local installer
ARG VERSION=local
# Some convenient keys for building, do not change these
ENV VERSION ${VERSION}
ENV PACKAGE_NAME ometascan-${VERSION}-1.x86_64.rpm
ENV WORK_DIR /mdcore
ENV PACKAGE_PATTERN ometascan-*.rpm
ENV PACKAGE_FILE ${WORK_DIR}/ometascan.rpm
# All designated data files and folders to be used by MetaDefender Core upon installed will reside inside
ENV INSTALL_ROOT /opt/ometascan
# MetaDefender Core internal configurations
ENV REST_PORT 8008
ENV IGNITION_FILE ${INSTALL_ROOT}/etc/opswat/ometascan.conf
ENV DATA_DIR ${INSTALL_ROOT}/var/lib/ometascan
ENV CORE_CONF ${INSTALL_ROOT}/etc/ometascan/ometascan.conf
# User for installing Core and running
ENV RUN_USER metascan
ENV RUN_GROUP metascan
ENV RUN_UID 1000
ENV RUN_GID 1000
# Define apikey path to store apikey for license activation and deactivation
ENV APIKEY_PATH ${INSTALL_ROOT}/etc/opswat/apikey

- `VERSION` variable needs to be set to the desired version of MetaDefender Core to be downloaded and used.
- `RUN_USER` variable is the user that is automatically created in the container and then used to run the MetaDefender Core. It could be non-root user.
- `INSTALL_ROOT` variable to define root folder for all MetaDefender Core data files and folder to reside inside.
- `APIKEY_PATH` variable to define file path containing API key of your desired local user admin on MetaDefender Core, that will be used for license activation and deactivation.
