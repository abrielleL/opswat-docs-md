<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-redis-airgapped -->

# Air-gapped

Requires Redis version 7.2 or later.

Info

To install Redis in an air-gapped environment, download the required packages on a **preparation machine** and then transfer them to the **air-gapped server**. The preparation machine should have internet access and run the **same operating system version** as the target server.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-redis-airgapped#prerequisites)

Before installing the Redis service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Rocky Linux 9+, or RHEL 9+. |
| Privileges | `root` or `sudo` privileges on both the preparation machine and the air-gapped server. |
| Hardware | 2 vCPU  32 GB RAM minimum. |
| Disk space | At least 50 GB of available storage. |
| Network access | Required port is open (default port: **6379**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |
| Offline Package Transfer | A USB drive or other secure transfer medium is required to move the packages to the air-gapped server. |

## [Debian, Ubuntu](/docs/mdcluster/installation/md-cluster-redis-airgapped#debian-ubuntu)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-redis-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_redis.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Build an offline Redis install bundle for an air-gapped Ubuntu/Debian host.
#
# Dependency resolution: apt resolves the FULL closure as if nothing were
# installed (Dir::State::status -> an empty file), so the bundle is complete
# regardless of what's on this build host - the apt equivalent of dnf's
# --alldeps. The real system is never touched (download-only + throwaway status).
set -euo pipefail
# ---- configuration ---------------------------------------------------------
# Pin the UPSTREAM Redis version (e.g. 8.6.4) - REQUIRED.
# The full apt version string - epoch, Debian revision and the codename suffix
# like "~noble1" - is detected automatically from the repo for THIS release,
# so the same script works unchanged on jammy / bookworm / etc.
REDIS_UPSTREAM="${REDIS_UPSTREAM:-8.6.4}"
INCLUDE_RECOMMENDS="${INCLUDE_RECOMMENDS:-yes}" # yes = also bundle Recommends
PKGS=(redis redis-server redis-tools)
ARCH="$(dpkg --print-architecture)"
. /etc/os-release
CODENAME="${VERSION_CODENAME:?cannot detect release codename}"
OUTDIR="$(pwd)/redis-offline"
# Empty status file = "nothing is installed" -> apt downloads every dependency.
EMPTY_STATUS="$(mktemp)"
trap 'rm -f "$EMPTY_STATUS"' EXIT
echo ">> target: Redis ${REDIS_UPSTREAM:-latest} | ${ID:-?} ${CODENAME} | ${ARCH}"
# ---- build-host tooling + Redis repository ---------------------------------
sudo apt-get update
sudo apt-get install -y --no-install-recommends curl gpg ca-certificates dpkg-dev
curl -fsSL https://packages.redis.io/gpg \
| sudo gpg --dearmor --yes -o /usr/share/keyrings/redis-archive-keyring.gpg
sudo chmod 644 /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb ${CODENAME} main" \
| sudo tee /etc/apt/sources.list.d/redis.list >/dev/null
sudo apt-get update
# ---- auto-detect the exact, codename-correct version -----------------------
# packages.redis.io serves a per-codename repo, and Ubuntu's own universe also
# ships a (different, older) redis-server, so we match BOTH the upstream version
# and the "~<codename>" suffix to land on the right .deb. madison lists newest
# first, so head -n1 wins.
SPECS=()
if [ -n "$REDIS_UPSTREAM" ]; then
esc="$(printf '%s' "$REDIS_UPSTREAM" | sed 's/[.[\*^$]/\\&/g')"
REDIS_VERSION="$(
apt-cache madison redis-server \
| awk -F'|' '{gsub(/ /,"",$2); print $2}' \
| grep -E "(^|:)${esc}-" \
| grep -F "~${CODENAME}" \
| head -n1
)"
if [ -z "$REDIS_VERSION" ]; then
echo "ERROR: no Redis ${REDIS_UPSTREAM} build found for '${CODENAME}'." >&2
echo "Available versions:" >&2
apt-cache madison redis-server | awk -F'|' '{print " " $2}' >&2
exit 1
fi
echo ">> resolved version: ${REDIS_VERSION}"
for p in "${PKGS[@]}"; do SPECS+=("${p}=${REDIS_VERSION}"); done
else
echo "ERROR: REDIS_UPSTREAM is required" >&2
exit 1
fi
REC_FLAG="--no-install-recommends"
[ "$INCLUDE_RECOMMENDS" = "yes" ] && REC_FLAG="--install-recommends"
# ---- download packages + full dependency closure ---------------------------
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR/partial"
# Preview the complete closure (every .deb, base libs included).
echo ">> resolving full dependency closure..."
apt-get install --print-uris -y $REC_FLAG \
-o Dir::State::status="$EMPTY_STATUS" \
"${SPECS[@]}" \
| grep -oP "(?<=')[^']*\.deb" > "$OUTDIR/manifest.txt" || true
echo ">> $(wc -l < "$OUTDIR/manifest.txt") package file(s) to download"
# download-only + the empty status file: every dependency is fetched, but the
# real system is never modified.
sudo apt-get install -y --download-only $REC_FLAG \
-o Dir::State::status="$EMPTY_STATUS" \
-o Dir::Cache::archives="$OUTDIR" \
"${SPECS[@]}"
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

BashCopychmod +x prepare_redis.sh
./prepare_redis.sh

3. Copy the `redis-offline` folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install Redis](/docs/mdcluster/installation/md-cluster-redis-airgapped#install-redis)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `redis-offline` folder to `/opt/redis-offline` . E.g:

BashCopysudo cp -r redis-offline /opt/redis-offline

2. Run the commands below.

BashCopy# Verify integrity:
cd /opt/redis-offline && sha256sum -c SHA256SUMS
# Register
echo "deb [trusted=yes] file:/opt/redis-offline ./" | sudo tee /etc/apt/sources.list.d/redis-offline.list
# Update using ONLY this source
sudo apt-get -o Dir::Etc::sourcelist="sources.list.d/redis-offline.list" -o Dir::Etc::sourceparts="/dev/null" update
# Install Redis.
sudo apt-get install -y redis-server redis-tools
sudo systemctl enable --now redis-server

3. Access Redis configuration file /etc/redis/redis.conf for editing.
4. Comment out the bind setting and set protected-mode option to no.

BashCopy...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

5. Restart Redis.

BashCopysudo systemctl restart redis-server

6. Run the command with Redis CLI.

BashCopyredis-cli ping

7. Confirm that the response returned is PONG.

PONG
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-redis-airgapped#rocky-rhel)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-redis-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_redis.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Build an offline Redis install bundle for an air-gapped Rocky/RHEL host.
#
# Note: `dnf download --resolve --alldeps` pulls the FULL dependency closure
# regardless of what's installed on this build host, so a clean machine is NOT
# required for completeness. The cost is a larger bundle (it grabs base libs
# too). The local-repo install step below keeps that safe: on the target you
# `dnf install <name>` and dnf installs only what's missing - it will NOT
# force-downgrade your base system.
set -euo pipefail
# ---- configuration ---------------------------------------------------------
# Pin the UPSTREAM Redis version (e.g. 8.6.4). Leave empty for the latest.
# The release tag (".el9") and arch are filled in automatically for THIS host.
REDIS_VERSION="${REDIS_VERSION:-8.6.4}"
ARCH="$(uname -m)"
EL_VERSION="$(rpm -E %{rhel})"
OUTDIR="$(pwd)/redis-offline"
echo ">> target: Redis ${REDIS_VERSION:-latest} | EL${EL_VERSION} | ${ARCH}"
# ---- build-host tooling ----------------------------------------------------
sudo dnf install -y dnf-plugins-core createrepo_c
# ---- Redis repository + GPG key --------------------------------------------
# baseurl tracks the EL major version; gpgkey lets dnf verify on its own.
sudo tee /etc/yum.repos.d/redis.repo >/dev/null <<EOF
[redis]
name=Redis
baseurl=https://packages.redis.io/rpm/rockylinux${EL_VERSION}
enabled=1
gpgcheck=1
gpgkey=https://packages.redis.io/gpg
EOF
curl -fsSL https://packages.redis.io/gpg -o /tmp/redis.key
sudo rpm --import /tmp/redis.key
sudo dnf makecache || true
# ---- resolve the exact, EL-correct NEVRA -----------------------------------
# (release tag like "1.el9" and the arch are appended automatically; newest
# matching release wins). On EL8 you'd also: sudo dnf module disable redis
SPEC="redis"
if [ -n "$REDIS_VERSION" ]; then
esc="$(printf '%s' "$REDIS_VERSION" | sed 's/[.[\*^$]/\\&/g')"
SPEC="$(
dnf repoquery --quiet --repo=redis --arch="${ARCH},noarch" \
--queryformat '%{name}-%{version}-%{release}.%{arch}' redis 2>/dev/null \
| grep -E -- "-${esc}-" \
| sort -V | tail -n1
)"
if [ -z "$SPEC" ]; then
echo "ERROR: no Redis ${REDIS_VERSION} build found for EL${EL_VERSION}/${ARCH}." >&2
echo "Available redis versions in the repo:" >&2
dnf repoquery --quiet --repo=redis redis \
--queryformat ' %{version}-%{release}.%{arch}' >&2
exit 1
fi
echo ">> resolved: ${SPEC}"
fi
# ---- download package + full dependency closure ----------------------------
# --resolve : also fetch dependencies
# --alldeps : fetch them even if already installed here (= complete bundle)
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR"
dnf download --resolve --alldeps --downloaddir "$OUTDIR" "$SPEC"
# ---- turn the folder into a local dnf repo ---------------------------------
# So the air-gapped install is a clean `dnf install <name>` with ordering and
# dependency *selection* handled for you. Do NOT `dnf install *.rpm` - that
# tries to install every base lib in the bundle and can downgrade the target.
createrepo_c "$OUTDIR"
# ---- bundle the GPG key + integrity manifest -------------------------------
cp -f /tmp/redis.key "$OUTDIR/RPM-GPG-KEY-redis"
( cd "$OUTDIR" && sha256sum *.rpm > SHA256SUMS )
echo
echo ">> done."
echo ">> bundle: $OUTDIR"
echo ">> files: $(ls "$OUTDIR"/*.rpm | wc -l) .rpm"
echo ">> size: $(du -sh "$OUTDIR" | cut -f1)"

2. Run commands.

BashCopychmod +x prepare_redis.sh
./prepare_redis.sh

3. Copy the redis folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install Redis](/docs/mdcluster/installation/md-cluster-redis-airgapped#install-redis)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `redis-offline` folder to `/opt/redis-offline` . E.g:

BashCopysudo cp -r redis-offline /opt/redis-offline

3. Run the commands below.

BashCopy# Verify integrity
cd /opt/redis-offline && sha256sum -c SHA256SUMS
# Install from the local folder as a temporary repo
sudo dnf install -y \
--disablerepo='*' \
--repofrompath=redisoffline,/opt/redis-offline \
--setopt=redisoffline.gpgcheck=0 \
redis

3. Access Redis configuration file `/etc/redis/redis.conf` for editing.
4. Comment out the `bind` setting and set `protected-mode` option to **no***.*

BashCopy...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

3. Restart Redis.

BashCopysudo systemctl restart redis

4. Run the command with Redis CLI.

BashCopyredis-cli ping

5. Confirm that the response returned is PONG.

PONG
