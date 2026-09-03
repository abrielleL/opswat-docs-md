<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped -->

# Air-gapped

Requires RabbitMQ version 4.2 or later, along with a compatible Erlang version.

Info

To install Redis in an air-gapped environment, download the required packages on a **preparation machine** and then transfer them to the **air-gapped server**. The preparation machine should have internet access and run the **same operating system version** as the target server.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#prerequisites)

Before installing the RabbitMQ service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Rocky Linux 9+, or RHEL 9+. |
| Privileges | `root` or `sudo` privileges on both the preparation machine and the air-gapped server. |
| Hardware | 4 vCPU and 8 GB RAM. |
| Disk space | At least 100 GB of available storage. |
| Network access | Required ports are open:   - **5672** — AMQP client connections (default). - **15672** — Management UI (optional).   A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |

## [Debian, Ubuntu](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#debian-ubuntu)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_rabbitmq.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Build an offline RabbitMQ (+ Erlang) install bundle for an air-gapped
# Ubuntu/Debian host.
#
# Dependency resolution: apt resolves the FULL closure as if nothing were
# installed (Dir::State::status -> an empty file), so every Erlang module AND
# its base-library dependencies are fetched regardless of what's on this build
# host - the apt equivalent of dnf's --alldeps. The real system is never
# touched (download-only + throwaway status file).
set -euo pipefail
# ---- configuration ---------------------------------------------------------
# Pin the UPSTREAM RabbitMQ version 4.2.5.
# The Debian revision ("-1") is detected automatically from the repo. apt then
# resolves a *compatible* Erlang version for you - don't pin Erlang by hand.
RABBITMQ_UPSTREAM="${RABBITMQ_UPSTREAM:-4.2.5}"
INCLUDE_RECOMMENDS="${INCLUDE_RECOMMENDS:-yes}" # yes = also bundle Recommends
# RabbitMQ's recommended trimmed Erlang set (no GUI/wx). Named explicitly
# because some are runtime-needed but only Recommended, not hard Depends.
ERLANG_PKGS=(
erlang-base erlang-asn1 erlang-crypto erlang-eldap erlang-ftp erlang-inets
erlang-mnesia erlang-os-mon erlang-parsetools erlang-public-key
erlang-runtime-tools erlang-snmp erlang-ssl erlang-syntax-tools
erlang-tftp erlang-tools erlang-xmerl
)
ARCH="$(dpkg --print-architecture)"
. /etc/os-release
DISTRO="${ID:?cannot detect distro}" # ubuntu | debian
CODENAME="${VERSION_CODENAME:?cannot detect release codename}"
KEYRING="/usr/share/keyrings/com.rabbitmq.team.gpg"
OUTDIR="$(pwd)/rabbitmq-offline"
# Empty status file = "nothing is installed" -> apt downloads every dependency.
EMPTY_STATUS="$(mktemp)"
trap 'rm -f "$EMPTY_STATUS"' EXIT
echo ">> target: RabbitMQ ${RABBITMQ_UPSTREAM:-latest} | ${DISTRO} ${CODENAME} | ${ARCH}"
# ---- build-host tooling ----------------------------------------------------
sudo apt-get update
sudo apt-get install -y --no-install-recommends curl gpg ca-certificates dpkg-dev
# ---- RabbitMQ signing key + repositories -----------------------------------
curl -1sLf "https://keys.openpgp.org/vks/v1/by-fingerprint/0A9AF2115F4687BD29803A206B73A36E6026DFCA" \
| sudo gpg --dearmor --yes -o "$KEYRING"
sudo chmod 644 "$KEYRING"
# Two mirrors each for Erlang and RabbitMQ; paths track distro + codename.
sudo tee /etc/apt/sources.list.d/rabbitmq.list >/dev/null <<EOF
## Modern Erlang/OTP releases
deb [arch=${ARCH} signed-by=${KEYRING}] https://deb1.rabbitmq.com/rabbitmq-erlang/${DISTRO}/${CODENAME} ${CODENAME} main
deb [arch=${ARCH} signed-by=${KEYRING}] https://deb2.rabbitmq.com/rabbitmq-erlang/${DISTRO}/${CODENAME} ${CODENAME} main
## Modern RabbitMQ releases
deb [arch=${ARCH} signed-by=${KEYRING}] https://deb1.rabbitmq.com/rabbitmq-server/${DISTRO}/${CODENAME} ${CODENAME} main
deb [arch=${ARCH} signed-by=${KEYRING}] https://deb2.rabbitmq.com/rabbitmq-server/${DISTRO}/${CODENAME} ${CODENAME} main
EOF
sudo apt-get update
# ---- resolve the exact rabbitmq-server version -----------------------------
RMQ_SPEC="rabbitmq-server"
if [ -n "$RABBITMQ_UPSTREAM" ]; then
esc="$(printf '%s' "$RABBITMQ_UPSTREAM" | sed 's/[.[\*^$]/\\&/g')"
RMQ_VER="$(
apt-cache madison rabbitmq-server \
| awk -F'|' '{gsub(/ /,"",$2); print $2}' \
| grep -E "(^|:)${esc}-" \
| head -n1
)"
if [ -z "$RMQ_VER" ]; then
echo "ERROR: no rabbitmq-server ${RABBITMQ_UPSTREAM} found for ${CODENAME}." >&2
echo "Available versions:" >&2
apt-cache madison rabbitmq-server | awk -F'|' '{print " " $2}' >&2
exit 1
fi
echo ">> resolved rabbitmq-server: ${RMQ_VER}"
RMQ_SPEC="rabbitmq-server=${RMQ_VER}"
fi
# rabbitmq-server is pinned; Erlang stays unpinned so apt picks compatible
# versions, and the whole set is solved together.
SPECS=("$RMQ_SPEC" "${ERLANG_PKGS[@]}")
REC_FLAG="--no-install-recommends"
[ "$INCLUDE_RECOMMENDS" = "yes" ] && REC_FLAG="--install-recommends"
# ---- download packages + full dependency closure ---------------------------
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR/partial"
# Preview the complete closure (rabbitmq-server + all Erlang modules + base libs).
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

BashCopychmod +x prepare_rabbitmq.sh
./prepare_rabbitmq.sh

3. Copy the `rabbitmq-offline` folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install RabbitMQ](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#install-rabbitmq)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `rabbitmq-offline` folder to `/opt/rabbitmq-offline`. E.g:

BashCopysudo cp -r rabbitmq-offline /opt/rabbitmq-offline

3. Run the commands below.

BashCopy# Verify integrity:
cd /opt/rabbitmq-offline && sha256sum -c SHA256SUMS
# Register it as a local apt repo:
echo "deb [trusted=yes] file:/opt/rabbitmq-offline ./" \
| sudo tee /etc/apt/sources.list.d/rabbitmq-offline.list
# Update using ONLY this source:
sudo apt-get -o Dir::Etc::sourcelist="sources.list.d/rabbitmq-offline.list" \
-o Dir::Etc::sourceparts="/dev/null" update
# Install
sudo apt-get install -y rabbitmq-server
sudo systemctl enable --now rabbitmq-server

4. Set up user.

BashCopysudo rabbitmqctl add_user <username> <password>
sudo rabbitmqctl set_permissions -p / <username> "." "." "."
sudo rabbitmqctl set_user_tags <username> administrator
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#rocky-rhel)

### [Prepare packages](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#prepare-packages)

1. On the preparation machine, create file `prepare_rabbitmq.sh` with content:

BashCopy#!/usr/bin/env bash
#
# Offline RabbitMQ bundle via GitHub releases - use this when the
# yum1/yum2.rabbitmq.com mirrors are unreachable from your build host but
# github.com AND the Rocky repos ARE reachable.
#
# How dependency resolution works here: the two RabbitMQ/Erlang RPMs come from
# GitHub (not a repo), so we stage them into a temporary local repo, then let
# dnf resolve their FULL dependency closure against that staging repo + the
# Rocky repos. That pulls ncurses-libs, openssl-libs, socat, logrotate, etc.
#
# RabbitMQ 4.2.x runs on Erlang 26.2.x or 27.x - verify at
# https://www.rabbitmq.com/docs/which-erlang
# and pick an available release from
# https://github.com/rabbitmq/erlang-rpm/releases
set -euo pipefail
# ---- configuration (check the GitHub releases pages for exact asset names) --
RABBITMQ_VERSION="${RABBITMQ_VERSION:-4.2.5}"
RABBITMQ_DIST="${RABBITMQ_DIST:-el8}" # server RPM is noarch; el8 installs fine on el9
ERLANG_VERSION="${ERLANG_VERSION:-27.2}" # MUST be compatible with the RabbitMQ version
ERLANG_DIST="${ERLANG_DIST:-el9}"
ARCH="${ARCH:-$(uname -m)}"
OUTDIR="$(pwd)/rabbitmq-offline"
RMQ_URL="https://github.com/rabbitmq/rabbitmq-server/releases/download/v${RABBITMQ_VERSION}/rabbitmq-server-${RABBITMQ_VERSION}-1.${RABBITMQ_DIST}.noarch.rpm"
ERL_URL="https://github.com/rabbitmq/erlang-rpm/releases/download/v${ERLANG_VERSION}/erlang-${ERLANG_VERSION}-1.${ERLANG_DIST}.${ARCH}.rpm"
echo ">> RabbitMQ ${RABBITMQ_VERSION} (${RABBITMQ_DIST}) + Erlang ${ERLANG_VERSION} (${ERLANG_DIST}/${ARCH})"
# ---- build-host tooling ----------------------------------------------------
sudo dnf install -y createrepo_c dnf-plugins-core curl
STAGE="$(mktemp -d)"
trap 'rm -rf "$STAGE"' EXIT
rm -rf "$OUTDIR"
mkdir -p "$OUTDIR"
# ---- fetch the two RPMs from GitHub into a staging repo --------------------
# curl -f makes a 404 fail loudly instead of saving an HTML error page as .rpm.
echo ">> downloading Erlang..."
curl -fL "$ERL_URL" -o "$STAGE/erlang-${ERLANG_VERSION}-1.${ERLANG_DIST}.${ARCH}.rpm"
echo ">> downloading RabbitMQ server..."
curl -fL "$RMQ_URL" -o "$STAGE/rabbitmq-server-${RABBITMQ_VERSION}-1.${RABBITMQ_DIST}.noarch.rpm"
# Verify they're real RPMs (not HTML error pages), then index as a local repo.
for f in "$STAGE"/*.rpm; do
rpm -qp "$f" >/dev/null 2>&1 || { echo "ERROR: $f is not a valid RPM (bad URL?)"; exit 1; }
done
createrepo_c "$STAGE"
# ---- resolve + download the FULL dependency closure ------------------------
# --resolve --alldeps : pull every dependency even if installed here, so the
# bundle is complete for a clean target.
# The staging repo provides rabbitmq-server + erlang; the Rocky repos provide
# their base-OS dependencies. Versions are pinned so we don't pick up Rocky's
# old SIG rabbitmq/erlang by mistake.
echo ">> resolving full dependency closure..."
dnf download --resolve --alldeps \
--repofrompath="rmqstage,$STAGE" \
--setopt=rmqstage.gpgcheck=0 \
--downloaddir "$OUTDIR" \
"rabbitmq-server-${RABBITMQ_VERSION}" "erlang-${ERLANG_VERSION}"
# ---- local repo + integrity manifest ---------------------------------------
createrepo_c "$OUTDIR"
( cd "$OUTDIR" && sha256sum *.rpm > SHA256SUMS )
echo
echo ">> done."
echo ">> bundle: $OUTDIR ($(ls "$OUTDIR"/*.rpm | wc -l) RPMs, $(du -sh "$OUTDIR" | cut -f1))"

2. Run commands.

BashCopychmod +x prepare_rabbitmq.sh
./prepare_rabbitmq.sh

3. Copy the rabbitmq-offline folder to a USB drive or secure transfer medium.
4. Move it to the air-gapped server.

### [Install RabbitMQ](/docs/mdcluster/installation/md-cluster-rabbitmq-airgapped#install-rabbitmq)

1. On the target server, insert the USB drive or secure transfer medium.
2. Copy `rabbitmq-offline` folder to `/opt/rabbitmq-offline`. E.g:

BashCopysudo cp -r rabbitmq-offline /opt/rabbitmq-offline

3. Run the commands below.

BashCopy# Verify integrity:
cd /opt/rabbitmq-offline && sha256sum -c SHA256SUMS
sudo dnf install -y \
--disablerepo='*' \
--repofrompath=rmqoffline,/opt/rabbitmq-offline \
--setopt=rmqoffline.gpgcheck=0 \
rabbitmq-server
sudo systemctl enable --now rabbitmq-server

4. Set up user.

BashCopysudo rabbitmqctl add_user <username> <password>
sudo rabbitmqctl set_permissions -p / <username> "." "." "."
sudo rabbitmqctl set_user_tags <username> administrator
