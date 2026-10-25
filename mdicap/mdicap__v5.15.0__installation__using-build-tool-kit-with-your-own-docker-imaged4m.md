<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/installation/using-build-tool-kit-with-your-own-docker-imaged4m -->

# Using build tool kit with your own docker image

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info

The docker build tool kit could be found on OPSWAT Portal - Products - Utilities

[**https://portal.opswat.com/products/utilities**](https://portal.opswat.com/products/utilities)

The build tool kit includes the following files:

- `Dockerfile` - main script for building the docker image.
- `entrypoint.sh` - startup script that runs when the container starts.
- `patch.sh` - utility script for string replacing in the file, needed for building docker image.
- `systemctl.py` (only applicable to CentOS) - the replacement for systemctl, needed for non-privileged container.

To build the image, just run the following command:

buildCopydocker build -t <image_name[:tag]> [--build-arg VERSION=<version>] <build-kit_path>

- `<image_name[:tag]>` - name of your built image with optional tag (e.g. `latest` ).
- `--build-arg VERSION=<version>`*-* the desired MetaDefender ICAP Server version to be downloaded from OPSWAT. If obmitted then a local installer will be used, the installer should be placed in the working directory with name is formatted /mdicapsrv/mdicapsrv-*.rpm or .deb (configurable in the Dockerfile).
- `<build-kit_path>` - relative path to your build-kit which contains Dockerfile.

For example:

buildCopydocker build -t mdicapsrv:centos --build-arg VERSION=4.13.0RC .

In Dockerfile, there are some environment variables that can be modified for various use cases. **You should modify the environment variables before building the MetaDefender ICAP Server docker image**.

confCopy# Product version for downloading installer package, ignored if use local installer
ARG VERSION=local
# User and path for installing ICAP and running
ENV RUN_USER mdicapsrv
ENV RUN_GROUP mdicapsrv
ENV RUN_UID 1000
ENV RUN_GID 1000
ENV INSTALL_ROOT /opt/mdicapsrv
# MetaDefender ICAP internal configurations
ENV REST_PORT 8048
ENV ICAP_PORT 1344
ENV ICAPS_PORT 11344
# Define apikey path to store apikey for deactivation
ENV APIKEY_PATH ${INSTALL_ROOT}/etc/opswat/apikey

- `VERSION` variable needs to be set to the desired version of MetaDefender ICAP Server to be downloaded and used.
- `RUN_USER` variable is the user that is automatically created in the container and then used to run the MetaDefender ICAP Server. It could be non-root user.
- `INSTALL_ROOT` variable to define root folder for all MetaDefender ICAP Server data files and folder to reside inside.
- `APIKEY_PATH` variable to define file path containing API key of your desired local user admin on MetaDefender ICAP Server, that will be used for license activation and deactivation.
