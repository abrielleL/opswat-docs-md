<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-redis-linux -->

# Linux

Requires Redis version 7.2 or later.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-redis-linux#prerequisites)

Before installing the Redis service, ensure the following requirements are met.

| Requirement | Description |
| --- | --- |
| Operating System | Debian 12+, Ubuntu 22.04+, Ubuntu 24.04+, Rocky Linux 9+, or RHEL 9+ |
| Privileges | `root` or `sudo` privileges. |
| Hardware | 2 vCPU  32 GB RAM minimum. |
| Disk space | At least 50 GB of available storage. |
| Network access | Required port is open (default port: **6379**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |

## [Debian/Ubuntu](/docs/mdcluster/installation/md-cluster-redis-linux#debianubuntu)

1. Add the repository to the APT index, update it, and install Redis:

BashCopy# add repository
sudo apt-get install lsb-release curl gpg
# get version code name. e.g: noble, jammy, ..
VERSION_CODENAME=$(lsb_release -cs)
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
sudo chmod 644 /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $VERSION_CODENAME main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt-get update
# install Redis
sudo apt-get install \
redis=6:8.6.4-1rl1~${VERSION_CODENAME}1 \
redis-server=6:8.6.4-1rl1~${VERSION_CODENAME}1 \
redis-tools=6:8.6.4-1rl1~${VERSION_CODENAME}1
sudo systemctl enable --now redis-server
# check redis-server status
sudo systemctl status redis-server

2. Access Redis configuration file `/etc/redis/redis.conf` for editing.
3. Comment out the `bind` setting and set `protected-mode` option to **no***.*

BashCopy...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

4. Restart Redis.

BashCopysudo systemctl restart redis-server

5. Run the command with Redis CLI.

BashCopyredis-cli ping

6. Confirm that the response returned is PONG.

PONG
## [Rocky, RHEL](/docs/mdcluster/installation/md-cluster-redis-linux#rocky-rhel)

1. Create the file `/etc/yum.repos.d/redis.repo` with the following contents.

[Redis]
name=Redis
baseurl=http://packages.redis.io/rpm/rockylinux9
enabled=1
gpgcheck=1

2. Run the commands.

BashCopycurl -fsSL https://packages.redis.io/gpg > /tmp/redis.key
sudo rpm --import /tmp/redis.key
sudo dnf install -y redis-8.6.4-1.x86_64
sudo systemctl enable --now redis
sudo systemctl status redis

3. Access Redis configuration file `/etc/redis/redis.conf` for editing.
4. Comment out the `bind` setting and set `protected-mode` option to **no.**

BashCopy...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

4. Restart Redis.

BashCopysudo systemctl restart redis

5. Run the command with Redis CLI.

BashCopyredis-cli ping

6. Confirm that the response returned is PONG.

PONG
