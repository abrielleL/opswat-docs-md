<!-- source: https://www.opswat.com/docs/mdcluster/configurations/redis-ha -->

# High Availability support for Redis

A minimum of **two** Redis instances must be installed on separate hosts for High Availability solution to function properly.

An **odd number** of **Redis Sentinels** should be installed.

### [Redis Sentinel](/docs/mdcluster/configurations/redis-ha#redis-sentinel)

1. Install Redis instances on servers.
2. Select one instance as primary. In **Linux Terminal** of the other instances (replicas), run the following command:

BashCopy# Debian/Ubuntu or Red Hat/Rocky
$ redis-cli replicaof <primary_host> <primary_port>

3. Build configuration file for **Redis Sentinel**.

BashCopy# The port on which the Sentinel should run
port <SENTINEL_PORT>
# By default Redis does not run as a daemon. Use 'yes' if you need it.
# Note that Redis will write a pid file in /var/run/redis.pid when daemonized.
daemonize yes
sentinel monitor myprimary <PRIMARY_IP> <PRIMARY_PORT> 2
# sentinel monitor <master-name> <ip> <port> <quorum>
# quorum is the number of Sentinels that need to agree about the
# fact the master is not reachable, in order to really mark the master as
# failing, and eventually start a failover procedure if possible.
sentinel down-after-milliseconds myprimary 2000
# means sentinel will consider master down after 2 seconds
sentinel failover-timeout myprimary 4000
# means the chosen sentinel has 4 seconds to perform failover
sentinel parallel-syncs myprimary 2
# sets the number of replicas that can be reconfigured to use the new master
# after a failover at the same time. The lower the number, the more time it
# will take for the failover process to complete, however if the replicas are
# configured to serve old data, you may not want all the replicas to
# re-synchronize with the master at the same time. While the replication process is
# mostly non blocking for a replica, there is a moment when it stops to
# load the bulk data from the master. You may want to make sure only one
# replica at a time is not reachable by setting this option to the value of 1.Info

Duplicate the configuration file and modify `SENTINEL_PORT` to the appropriate port that the Redis Sentinel instance listens on.

4. Install Redis Sentinel instances on servers with the corresponding configuration files.

BashCopy# Debian/Ubuntu or Red Hat/Rocky
$ sudo redis-server </path/to/sentinel-config-file> --sentinel

5. Verify the Redis primary and its replicas. In **Linux Terminal** of any machine, run the following command:

BashCopy# Debian/Ubuntu or Red Hat/Rocky
$ redis-cli -h <sentinel_host> -p <sentinel_port>
# Provides information about the Primary
> sentinel master myprimary
# Gives you information about the replicas connected to the Primary
> sentinel replicas myprimary
# Provides information on the other Sentinels
> sentinel sentinels myprimary
# Provides the IP address of the current Primary
> sentinel get-master-addr-by-name myprimary
### [Setup instructions](/docs/mdcluster/configurations/redis-ha#setup-instructions)

1. Sign to MD Cluster **Control Center** console with your Administrator account.
2. Navigate to `Inventory` > `Services`.
3. Expand the `Redis` group.
4. Click `Add service`.
5. Enter the values for `Name`, `Host`, `Port`, `Username` and `Password` fields of individual Redis instance.

Warning

MD Cluster Control Center **only accepts Redis** and **not Redis Sentinel**.

6. Click the Check icon in the bottom right to complete.
7. Ensure all RabbitMQ nodes are reachable by the MD Cluster **Control Center**.
