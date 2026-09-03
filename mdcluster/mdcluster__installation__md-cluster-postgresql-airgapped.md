<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-postgresql-airgapped -->

# Air-gapped

Requires PostgreSQL version 16.9 or later.

Info

To install PostgreSQL in an air-gapped environment, download the required packages on a **preparation machine** and then transfer them to the **air-gapped server**. The preparation machine should have internet access and run the **same operating system version** as the target server.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#prerequisites)

Before installing the PostgreSQL service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Rocky Linux 9+, or RHEL 9+. |
| Privileges | `root` or `sudo` privileges on both the preparation machine and the air-gapped server. |
| Hardware | Minimum 8 vCPU and 16 GB RAM. |
| Disk space | At least 1 TB of available storage on **SSD** or **NVMe** for optimal performance.  Approximately 4 GB of storage is required per 1 million scanned objects for a deployment with 5 MD Core instances running 8 AV engines each. |
| Network access | Required port is open (default port: **5432**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |
| Offline Package Transfer | A USB drive or other secure transfer medium is required to move the packages to the air-gapped server. |

## [Debian, Ubuntu](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#debian-ubuntu)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_postgresql.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Build an offline PostgreSQL install bundle for an air-gapped host.
#
# Dependency resolution: apt resolves the FULL closure as if nothing were
# installed (Dir::State::status -> an empty file), so the bundle is complete
# regardless of what's on this build host - the apt equivalent of dnf's
# --alldeps. The real system is never touched (download-only + a throwaway
# status file).
set -euo pipefail
# ---- configuration ---------------------------------------------------------
PG_VERSION="${PG_VERSION:-16}" # PostgreSQL major version
INCLUDE_RECOMMENDS="${INCLUDE_RECOMMENDS:-yes}" # yes = bundle Recommends too
PACKAGES=("postgresql-${PG_VERSION}" "postgresql-contrib")
ARCH="$(dpkg --print-architecture)"
. /etc/os-release
CODENAME="${VERSION_CODENAME:?cannot detect release codename}"
OUTDIR="$(pwd)/postgresql-offline"
# Empty status file = "nothing is installed" -> apt downloads every dependency.
EMPTY_STATUS="$(mktemp)"
trap 'rm -f "$EMPTY_STATUS"' EXIT
echo ">> target: PostgreSQL ${PG_VERSION} | ${ID:-?} ${CODENAME} | ${ARCH}"
# ---- host tooling ----------------------------------------------------------
sudo apt-get update
sudo apt-get install -y --no-install-recommends \
postgresql-common dpkg-dev ca-certificates
# ---- PGDG repository (key + sources, configured once) ----------------------
# The official script configures BOTH the signing key and the deb822 sources
# file for the right codename/arch. Don't also hand-write sources.list - doing
# both is what causes "duplicate source" and key-mismatch errors.
echo "" | sudo /usr/share/postgresql-common/pgdg/apt.postgresql.org.sh
sudo apt-get update
# ---- download packages + full dependency closure ---------------------------
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR/partial"
REC_FLAG="--no-install-recommends"
[ "$INCLUDE_RECOMMENDS" = "yes" ] && REC_FLAG="--install-recommends"
# Preview the complete closure (every .deb, base libs included).
echo ">> resolving full dependency closure..."
apt-get install --print-uris -y $REC_FLAG \
-o Dir::State::status="$EMPTY_STATUS" \
"${PACKAGES[@]}" \
| grep -oP "(?<=')[^']*\.deb" > "$OUTDIR/manifest.txt" || true
echo ">> $(wc -l < "$OUTDIR/manifest.txt") package file(s) to download"
# Download them. download-only + the empty status file means the real system
# is never modified, but every dependency is fetched into the bundle.
sudo apt-get install -y --download-only $REC_FLAG \
-o Dir::State::status="$EMPTY_STATUS" \
-o Dir::Cache::archives="$OUTDIR" \
"${PACKAGES[@]}"
# apt leaves lock/partial artifacts behind - drop them and fix ownership.
sudo rm -rf "$OUTDIR/partial" "$OUTDIR/lock"
sudo chown -R "$(id -u):$(id -g)" "$OUTDIR"
# ---- turn the folder into a local apt repo ---------------------------------
# So the air-gapped install becomes a clean `apt-get install` that pulls only
# what the target actually needs (far safer than `dpkg -i *.deb`).
( cd "$OUTDIR" \
&& dpkg-scanpackages -m . /dev/null > Packages \
&& gzip -9c Packages > Packages.gz )
# ---- integrity manifest ----------------------------------------------------
( cd "$OUTDIR" && sha256sum *.deb > SHA256SUMS )
echo
echo ">> done."
echo ">> bundle: $OUTDIR"
echo ">> files: $(ls "$OUTDIR"/*.deb | wc -l) .deb"
echo ">> size: $(du -sh "$OUTDIR" | cut -f1)"

2. Run commands.

BashCopychmod +x prepare_postgresql.sh
./prepare_postgresql.sh

3. Copy the `postgresql-offline` folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install PostgreSQL](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#install-postgresql)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `postgresql-offline` folder to `/opt/postgresql-offline` . E.g:

BashCopysudo cp -r postgresql-offline /opt/postgresql-offline

3. Run the commands below.

BashCopy# Verify integrity:
cd /opt/postgresql-offline && sha256sum -c SHA256SUMS
# Register it as a local apt repo:
echo "deb [trusted=yes] file:/opt/postgresql-offline ./" \
| sudo tee /etc/apt/sources.list.d/pg-offline.list
# Update using ONLY this source
sudo apt-get -o Dir::Etc::sourcelist="sources.list.d/pg-offline.list" \
-o Dir::Etc::sourceparts="/dev/null" update
# Install
sudo apt-get install -y postgresql-16
# Configures PostgreSQL to start automatically whenever the system boots
sudo systemctl enable --now postgresql
# Setup login password
sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '<your_password>';"
### [Open connection](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#open-connection)

1. Locate the PostgreSQL data directory on your server.

BashCopy/etc/postgresql/16/main/

2. To allow remote connections, open the **postgresql.conf** file and configure the following setting:

postgresql.confCopylisten_addresses = '*'

3. To allow MetaDefender Cluster services to access the database, open the **p g_hba.conf** file and add the following rule.

pg_hba.confCopyhostssl all all 0.0.0.0/0 scram-sha-256

4. Restart the PostgreSQL service to apply the changes.

BashCopysudo systemctl restart postgresql
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#rocky-rhel)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_postgresql.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Build an offline PostgreSQL install bundle for an air-gapped Rocky/RHEL host.
#
# `dnf download --resolve --alldeps` pulls the FULL dependency closure
# regardless of what's installed on this build host, so a clean machine is NOT
# required for completeness. The cost is a larger bundle (it grabs base libs
# too). The local-repo install step keeps that safe: on the target you
# `dnf install <name>` and dnf installs only what's missing - it will NOT
# force-downgrade your base system.
set -euo pipefail
# ---- configuration ---------------------------------------------------------
PG_VERSION="${PG_VERSION:-16}" # PostgreSQL major version
PACKAGES=("postgresql${PG_VERSION}-server" "postgresql${PG_VERSION}-contrib")
ARCH="$(uname -m)"
EL_VERSION="$(rpm -E %{rhel})"
OUTDIR="$(pwd)/postgresql-offline"
REPO_RPM="https://download.postgresql.org/pub/repos/yum/reporpms/EL-${EL_VERSION}-${ARCH}/pgdg-redhat-repo-latest.noarch.rpm"
echo ">> target: PostgreSQL ${PG_VERSION} | EL${EL_VERSION} | ${ARCH}"
# ---- build-host tooling ----------------------------------------------------
sudo dnf install -y dnf-plugins-core createrepo_c
# ---- PGDG repository + disable the built-in AppStream module ---------------
sudo dnf install -y "$REPO_RPM"
sudo dnf -qy module disable postgresql
# ---- download packages + full dependency closure ---------------------------
# --resolve : also fetch dependencies
# --alldeps : fetch them even if already installed here (= complete bundle)
# Run as your normal user so the .rpm files aren't root-owned.
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR"
dnf download --resolve --alldeps --downloaddir "$OUTDIR" "${PACKAGES[@]}"
# ---- turn the folder into a local dnf repo ---------------------------------
# So the air-gapped install is a clean `dnf install <name>` with ordering and
# dependency *selection* handled for you. Do NOT `dnf install *.rpm` - that
# tries to install every base lib in the bundle and can downgrade the target.
createrepo_c "$OUTDIR"
# ---- bundle the PGDG GPG key + integrity manifest --------------------------
cp -f /etc/pki/rpm-gpg/*PGDG* "$OUTDIR"/ 2>/dev/null || true
( cd "$OUTDIR" && sha256sum *.rpm > SHA256SUMS )
echo
echo ">> done."
echo ">> bundle: $OUTDIR"
echo ">> files: $(ls "$OUTDIR"/*.rpm | wc -l) .rpm"
echo ">> size: $(du -sh "$OUTDIR" | cut -f1)"

2. Run commands.

BashCopychmod +x prepare_postgresql.sh
./prepare_postgresql.sh

3. Copy the postgresql-offline folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install PostgreSQL](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#install-postgresql)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `postgresql-offline` folder to `/opt/postgresql-offline` . E.g:

BashCopysudo cp -r postgresql-offline /opt/postgresql-offline

3. Run the commands below.

BashCopy# Verify integrity:
cd /opt/postgresql-offline && sha256sum -c SHA256SUMS
# Disable the built-in module here too (it conflicts with PGDG)
sudo dnf -qy module disable postgresql
# Install
sudo dnf install -y \
--disablerepo='*' \
--repofrompath=pgoffline,/opt/postgresql-offline \
--setopt=pgoffline.gpgcheck=0 \
postgresql16-server postgresql16-contrib
# Configures PostgreSQL to start automatically whenever the system boots
sudo /usr/pgsql-16/bin/postgresql-16-setup initdb
# Configures PostgreSQL to start automatically whenever the system boots
sudo systemctl enable --now postgresql-16
# Setup login password
sudo -u postgres psql -c "ALTER USER postgres WITH PASSWORD '<your_password>';"
### [Open connection](/docs/mdcluster/installation/md-cluster-postgresql-airgapped#open-connection)

1. Locate the PostgreSQL data directory on your server.

BashCopy/var/lib/pgsql/16/data

2. To allow remote connections, open the **postgresql.conf** file and configure the following setting:

postgresql.confCopylisten_addresses = '*'

3. To allow MetaDefender Cluster services to access the database, open the **pg_hba.conf** file and add the following rule.

pg_hba.confCopyhost all all 0.0.0.0/0 scram-sha-256

4. Restart the PostgreSQL service to apply the changes.

BashCopysudo systemctl restart postgresql-16
