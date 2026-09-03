<!-- source: https://www.opswat.com/docs/mdcluster/trouble-shooting/collect-log-support-package -->

# Log Gathering in MetaDefender Cluster

## [Download support packages](/docs/mdcluster/trouble-shooting/collect-log-support-package#download-support-packages)

From the web console of MetaDefender Cluster (MD Cluster), the administrator can easily download the support packages of the following services:

- MD Cluster **Control Center**
- MD Cluster **Identity Service**
- MD Cluster **File Storage**
- MD Cluster **Worker** including MD Cluster **API Gateway**, MD Cluster **Callback Service** or **MetaDefender Core** deployed by the worker.

Please refer to [Remote Support Package Gathering](/docs/mdcluster/configurations/remote-support-package-gathering) for more information.

## [Collect service logs](/docs/mdcluster/trouble-shooting/collect-log-support-package#collect-service-logs)

Logs from the services Redis, RabbitMQ, and PostgreSQL need to be collected manually.

### [Redis - Caching Server](/docs/mdcluster/trouble-shooting/collect-log-support-package#redis---caching-server)

Info

Redis caching server is officially supported on Linux.

1. Run Terminal as root privilege (`sudo`).
2. Open Redis config file `/etc/redis/redis.conf` in edit mode e.g.:

BashCopy$ vi /etc/redis/redis.conf

3. Find and replace `logfile` directive with your desired location.

BashCopylogfile "<path/to/your/redis/log>.log"

4. Save the file, and restart Redis daemon.

BashCopy$ sudo systemctl restart redis

5. Find and collect Redis log `<path/to/your/redis/log>.log`

### [RabbitMQ - Message Broker Server](/docs/mdcluster/trouble-shooting/collect-log-support-package#rabbitmq---message-broker-server)

#### [Windows](/docs/mdcluster/trouble-shooting/collect-log-support-package#windows)

1. Locate and collect RabbitMQ log files that match the pattern `%APPDATA%\RabbitMQ\log\rabbit@<computer name>.log`.
2. Locate and collect RabbitMQ upgrade log files that match the pattern `%APPDATA%\RabbitMQ\log\rabbit@<computer name>_upgrade.log`.

#### [Linux](/docs/mdcluster/trouble-shooting/collect-log-support-package#linux)

1. Run terminal as root privilege (`sudo`).
2. Run following command to retrieve RabbitMQ log location:

BashCopy$ rabbitmq-diagnostics -q log_location

3. Access RabbitMQ log folder and find log files:

   - `rabbit@<computer name>.log`
   - `rabbit@<computer name>_upgrade.log`

### [PostgreSQL - Database Server](/docs/mdcluster/trouble-shooting/collect-log-support-package#postgresql---database-server)

#### [Windows](/docs/mdcluster/trouble-shooting/collect-log-support-package#windows)

1. Locate and collect log files that match the pattern `C:\Program Files\PostgreSQL\12\data\log with names postgresql-<yyyy-mm-dd>_<HHMMSS>.log`

#### [Linux](/docs/mdcluster/trouble-shooting/collect-log-support-package#linux)

1. Run terminal as root privilege (`sudo`).
2. Open the PostgreSQL config file `/etc/postgresql/12/main/postgresql.conf` in edit mode e.g.:

BashCopy$ vi /etc/postgresql/12/main/postgresql.conf

3. Find and turn `logging_collector` directive on :

BashCopylogging_collector = on

4. Save the file and restart PostgreSQL daemon, e.g.:

BashCopy$ sudo systemctl restart postgresql

5. Locate and collect log files that match the pattern `/var/lib/postgresql/12/main/log/postgresql-<yyyy-mm-dd>_<HHMMSS>.log`.
