<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-rabbitmq-linux -->

# Linux

Requires RabbitMQ version 4.2 or later.

Please refer to [the link](https://www.rabbitmq.com/docs/which-erlang#compatibility-matrix) for the Erlang-RabbitMQ compatibility matrix.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#prerequisites)

Before installing the RabbitMQ service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Ubuntu 24.04+, Rocky Linux 9+, or RHEL 9+ |
| Privileges | `root` or `sudo` privileges. |
| Hardware | 4 vCPU and 8 GB RAM. |
| Disk space | At least 100 GB of available storage. |
| Network access | Required ports are open:   - **5672** — AMQP client connections (default). - **15672** — Management UI (optional).   A minimum network bandwidth of **1 Gbps** is required. |

## [Ubuntu, Debian](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#ubuntu-debian)

### [Install Dependencies](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-dependencies)

BashCopysudo apt-get update -y
sudo apt-get install curl gnupg apt-transport-https wget -y
sudo apt-get install logrotate init-system-helpers adduser -y
### [Add Repository Signing Key](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#add-repository-signing-key)

BashCopy## Team RabbitMQ's signing key
curl -1sLf "https://keys.openpgp.org/vks/v1/by-fingerprint/0A9AF2115F4687BD29803A206B73A36E6026DFCA" | sudo gpg --dearmor | sudo tee /usr/share/keyrings/com.rabbitmq.team.gpg > /dev/null
### [Install Erlang/OTP](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-erlangotp)

1. Add a repository file.

- Ubuntu 24.4

BashCopysudo tee /etc/apt/sources.list.d/rabbitmq.list <<EOF
## Modern Erlang/OTP releases
##
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb1.rabbitmq.com/rabbitmq-erlang/ubuntu/noble noble main
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb2.rabbitmq.com/rabbitmq-erlang/ubuntu/noble noble main
## Provides modern RabbitMQ releases
##
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb1.rabbitmq.com/rabbitmq-server/ubuntu/noble noble main
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb2.rabbitmq.com/rabbitmq-server/ubuntu/noble noble main
EOF

- Debian Bookworm

BashCopysudo tee /etc/apt/sources.list.d/rabbitmq.list <<EOF
## Modern Erlang/OTP releases
##
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb1.rabbitmq.com/rabbitmq-erlang/debian/bookworm bookworm main
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb2.rabbitmq.com/rabbitmq-erlang/debian/bookworm bookworm main
## Provides modern RabbitMQ releases
##
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb1.rabbitmq.com/rabbitmq-server/debian/bookworm bookworm main
deb [arch=amd64 signed-by=/usr/share/keyrings/com.rabbitmq.team.gpg] https://deb2.rabbitmq.com/rabbitmq-server/debian/bookworm bookworm main
EOF

2. After updating the list of `apt` sources, it is necessary to run `apt-get update` .

BashCopysudo apt-get update -y

3. Install Erlang.

BashCopy## Install Erlang packages
sudo apt-get install -y erlang-base \
erlang-asn1 \
erlang-crypto \
erlang-eldap \
erlang-ftp \
erlang-inets \
erlang-mnesia \
erlang-os-mon \
erlang-parsetools \
erlang-public-key \
erlang-runtime-tools \
erlang-snmp \
erlang-ssl \
erlang-syntax-tools \
erlang-tftp \
erlang-tools \
erlang-xmerl
### [Install RabbitMQ](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-rabbitmq)

1. Run the following commands.

BashCopy# download the package
sudo apt-get -y install wget
sudo wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server_4.2.5-1_all.deb
# install the package with dpkg
sudo dpkg -i rabbitmq-server_4.2.5-1_all.deb
sudo rm rabbitmq-server_4.2.5-1_all.deb
sudo systemctl enable --now rabbitmq-server
sudo systemctl status rabbitmq-server

2. Set up user.

BashCopysudo rabbitmqctl add_user <username> <password>
sudo rabbitmqctl set_permissions -p / <username> "." "." "."
sudo rabbitmqctl set_user_tags <username> administrator
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#rocky-rhel)

### [Install Dependencies](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-dependencies)

BashCopysudo dnf install -y logrotate wget
### [Import the Signing Keys](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#import-the-signing-keys)

BashCopy## primary RabbitMQ signing key
sudo rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc'
## modern Erlang repository
sudo rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key'
## RabbitMQ server repository
sudo rpm --import 'https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key'
### [Add Yum Repositories](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#add-yum-repositories)

Create the file `/etc/yum.repos.d/rabbitmq.repo` with the following content.

BashCopy# In /etc/yum.repos.d/rabbitmq.repo
##
## Zero dependency Erlang RPM
##
[modern-erlang]
name=modern-erlang-el9
# Use a set of mirrors maintained by the RabbitMQ core team.
# The mirrors have significantly higher bandwidth quotas.
baseurl=https://yum1.rabbitmq.com/erlang/el/9/$basearch
https://yum2.rabbitmq.com/erlang/el/9/$basearch
repo_gpgcheck=1
enabled=1
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md
[modern-erlang-noarch]
name=modern-erlang-el9-noarch
# Use a set of mirrors maintained by the RabbitMQ core team.
# The mirrors have significantly higher bandwidth quotas.
baseurl=https://yum1.rabbitmq.com/erlang/el/9/noarch
https://yum2.rabbitmq.com/erlang/el/9/noarch
repo_gpgcheck=1
enabled=1
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-erlang.E495BB49CC4BBE5B.key
https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md
##
## RabbitMQ Server
##
[rabbitmq-el9]
name=rabbitmq-el9
baseurl=https://yum2.rabbitmq.com/rabbitmq/el/9/$basearch
https://yum1.rabbitmq.com/rabbitmq/el/9/$basearch
repo_gpgcheck=1
enabled=1
# Cloudsmith's repository key and RabbitMQ package signing key
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key
https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md
[rabbitmq-el9-noarch]
name=rabbitmq-el9-noarch
baseurl=https://yum2.rabbitmq.com/rabbitmq/el/9/noarch
https://yum1.rabbitmq.com/rabbitmq/el/9/noarch
repo_gpgcheck=1
enabled=1
# Cloudsmith's repository key and RabbitMQ package signing key
gpgkey=https://github.com/rabbitmq/signing-keys/releases/download/3.0/cloudsmith.rabbitmq-server.9F4587F226208342.key
https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
gpgcheck=1
sslverify=1
sslcacert=/etc/pki/tls/certs/ca-bundle.crt
metadata_expire=300
pkg_gpgcheck=1
autorefresh=1
type=rpm-md
### [Install Erlang](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-erlang)

BashCopysudo dnf update -y
sudo dnf install -y erlang
### [Install RabbitMQ](/docs/mdcluster/installation/md-cluster-rabbitmq-linux#install-rabbitmq)

1. Run the following commands.

BashCopyrpm --import https://github.com/rabbitmq/signing-keys/releases/download/3.0/rabbitmq-release-signing-key.asc
sudo wget https://github.com/rabbitmq/rabbitmq-server/releases/download/v4.2.5/rabbitmq-server-4.2.5-1.el8.noarch.rpm
sudo dnf install -y rabbitmq-server-4.2.5-1.el8.noarch.rpm
sudo rm abbitmq-server-4.2.5-1.el8.noarch.rpm
sudo systemctl enable --now rabbitmq-server
sudo systemctl status rabbitmq-server

2. Set up user.

BashCopysudo rabbitmqctl add_user <username> <password>
sudo rabbitmqctl set_permissions -p / <username> "." "." "."
sudo rabbitmqctl set_user_tags <username> administrator
