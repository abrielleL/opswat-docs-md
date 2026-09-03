<!-- source: https://www.opswat.com/docs/mdicap/installation/non-root-supportr2m -->

# Non-root support

## [How to run the container with non-root access via Docker Container](/docs/mdicap/installation/non-root-supportr2m#how-to-run-the-container-with-non-root-access-via-docker-container)

**Step 1**: get the docker image from docker hub (Refer to: [Docker image published on OPSWAT Docker Hub](/docs/mdicap/installation/docker-image-published-on-opswat-docker-hubd93))

**Step 2**: launch docker image with non-root option

Info

- specific **UID:GID = 1000:1000** to enable non-root support
- beside that, below environment variable require to run the doc

  - MD_USER=admin
  - MD_PWD=admin
  - ACCEPT_EULA=true
  - DB_USER=postgres
  - DB_PWD=postgres
  - DB_MODE=1
  - DB_HOST=localhost
  - DB_PORT=5432
  - DB_TYPE=local
BashCopydocker run --user 1000:1000 -it \
-e MD_USER=admin -e MD_PWD=admin \
-e ACCEPT_EULA=true -e DB_HOST=localhost \
-e DB_MODE=1 -e DB_TYPE=local -e DB_USER=postgres -e DB_PWD=posgres \
-e DB_PORT=5432 opswat/metadefendericapsrv-debian:5.8.0

**Step 3**: verify the UID:GID works properly

run command inside container to see the process mdicapsrv is running

BashCopyps -ef

## [How to customer the UID and GID value?](/docs/mdicap/installation/non-root-supportr2m#how-to-customer-the-uid-and-gid-value)

The default value of UID and GID is 1000, these default value can be customized via Docker toolkit on [My OPSWAT Portal](https://my.opswat.com/portal/home/) and rebuild a new image (refer to [Using build tool kit with your own docker image](/docs/mdicap/installation/using-build-tool-kit-with-your-own-docker-imaged4m))

**Step 1**: modify RUN_UID and RUN_GID value in file **Dockerfile**

**Step 2**: Rebuild docker image

BashCopycd <build-kit-directory>
docker build --build-arg VERSION=5.8.0 -t oharbor.opswat.com/icap/mdicapsrv-debian:5.8.0 .
