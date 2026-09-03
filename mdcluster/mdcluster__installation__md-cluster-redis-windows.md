<!-- source: https://www.opswat.com/docs/mdcluster/installation/md-cluster-redis-windows -->

# Windows

Requires Redis version 7.2 or later.

## [Prerequisites](/docs/mdcluster/installation/md-cluster-redis-windows#prerequisites)

| Requirement | Description |
| --- | --- |
| Operating System | Windows 11 23H2+, or Windows Server 2019+. |
| Privileges | Administrator privileges. |
| Hardware | 2 vCPU  32 GB RAM minimum. |
| Disk space | At least 50 GB of available storage. |
| Network access | Required port is open (default port: **6379**).  A minimum network bandwidth of **1 Gbps** is required.  A bandwidth of **5 Gbps or higher is strongly recommended** for production deployments. |

## [Windows Subsystem for Linux (WSL)](/docs/mdcluster/installation/md-cluster-redis-windows#windows-subsystem-for-linux-wsl)

#### [Install Windows Subsystem](/docs/mdcluster/installation/md-cluster-redis-windows#install-windows-subsystem)

1. Open **PowerShell as Administrator**.
2. Run the following command:

BashCopywsl --install

3. After launching, **Ubuntu** will open automatically and ask you to create a **Linux username and password**.
4. Update the Linux packages.

#### [Install Redis](/docs/mdcluster/installation/md-cluster-redis-windows#install-redis)

1. Add the repository to the APT index, update it, and install Redis:

BashCopy# add repository
sudo apt-get install lsb-release curl gpg
curl -fsSL https://packages.redis.io/gpg | sudo gpg --dearmor -o /usr/share/keyrings/redis-archive-keyring.gpg
sudo chmod 644 /usr/share/keyrings/redis-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/redis-archive-keyring.gpg] https://packages.redis.io/deb $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/redis.list
sudo apt-get update
# install Redis
sudo apt-get install \
redis=6:8.6.4-1rl1~noble1 \
redis-server=6:8.6.4-1rl1~noble1 \
redis-tools=6:8.6.4-1rl1~noble1
sudo systemctl enable --now redis-server
# check redis-server status
sudo systemctl status redis-server

2. Access Redis configuration file `/etc/redis/redis.conf` for editing.
3. Comment out the `bind` setting and set `protected-mode` option to **no.**

BashCopy...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

3. Restart Redis

BashCopysudo systemctl restart redis-server

4. Run the command with Redis CLI

BashCopyredis-cli ping

5. Confirm that the response returned is PONG

PONG
## [Memurai](/docs/mdcluster/installation/md-cluster-redis-windows#memurai)

#### [Download and install](/docs/mdcluster/installation/md-cluster-redis-windows#download-and-install)

1. Go to the official website: <https://www.memurai.com/get-memurai>
2. Choose the appropriate version.
3. Download the Windows installer (.msi).
4. Double-click the downloaded .msi file.

5. Click `Next` and follow the installation wizard.

- Accept the license agreement.
- Choose the installation directory.
- Select port (default is 6379).
- Click `Install` to start installation process.

#### [Verify Memurai installation](/docs/mdcluster/installation/md-cluster-redis-windows#verify-memurai-installation)

1. Open **Command Prompt** or **PowerShell**.
2. Run the command with Memurai CLI:

BashCopymemurai-cli ping

3. Confirm that the response returned is **PONG**.

BashCopyPONG
#### [Configure Memurai](/docs/mdcluster/installation/md-cluster-redis-windows#configure-memurai)

1. Access the Memurai configuration file in the installation directory, for example: `C:\Program Files\Memurai\memurai.conf`.
2. Comment out the `bind` setting and set `protected-mode` option to **no**.

...
# The following line should be commented
# bind 127.0.0.1
...
# The following line should be uncommented and set to no
protected-mode no
...

3. Restart Memurai service.
