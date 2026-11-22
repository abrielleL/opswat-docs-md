<!-- source: https://www.opswat.com/docs/supply-chain/troubleshooting/troubleshooting -->

# Troubleshooting

In this section, you can find solutions for common issues with MetaDefender Software Supply Chain.

### Running behind a proxy

If you need to deploy MetaDefender Software Supply Chain behind a proxy please consider the following:

- *.docker.io needs to be accessible in order to download the code
- [activation.dl.opswat.com](http://activation.dl.opswat.com/) needs to be accessible in order to activate the license
- the service unit you plan to integrate with needs to be accessible such that MetaDefender Software Supply Chain can access its APIs for different operations (e.g. file discovery, user listing, file download, file upload, file deletion, file renaming, etc.)

You will need to edit **/etc/mdssc/customer.env** and add the following environment variables to use a proxy server:

```bash
HTTP_PROXY="http://proxy_ip:proxy_port"
HTTPS_PROXY="https://proxy_ip:proxy_port"

no_proxy=api,binaries,bitbucket,commonservices,identityservice,containers,dockerhub,ecr,frontend,github,licensingservice,mongodb,mongomigrations,notifications,rabbitmq,rediscache,sourcecode
```

If a proxy is required to access to docker hub in order to pull MDSSC images, then this guide should be followed: [https://docs.docker.com/network/proxy/](https://docs.docker.com/network/proxy/)

The following section contain detailed instructions on how to troubleshoot or generate a support package based on your Unix operating system type.

### Collecting diagnostics

Run these commands as root, from any directory. The archives are written to `/etc/mdssc/`. For all commands, see [mdssc command line](https://www.opswat.com/docs/supply-chain/installation/mdssc-command-line).

| Situation | Command | Output |
| ---- | ---- | ---- |
| Quick health check | `sudo mdssc status` | Screen |
| Check the image versions | `sudo mdssc version` | Screen |
| First look at a problem | `sudo mdssc support` | Screen |
| Recent logs for a support ticket | `sudo mdssc support logs` | `support_logs_<time>.tar.gz` |
| Full package for engineering | `sudo mdssc support full` | `mdssc_<version>_support_package_<time>.tar` |
| Reproduce a problem with more detail | `sudo mdssc debug <service>` | Debug-level logs |

The example outputs below come from a test system. The names, sizes and times on your system are different.

#### 1. Health check

```bash
sudo mdssc status
```

Shows each container with its state, its restart count and a note if it was killed because it ran out of memory. It also shows disk use for `/etc/mdssc`, `/var/log` and the Docker data directory, and marks a disk above 90% used. For the full readiness check, run `sudo mdssc -c status`.

Example output:

```text
 MetaDefender Software Supply Chain 4.3.0

 CONTAINER            STATUS                   NOTE
 mdcs_rabbitmq        Up 3 days (healthy)
 mdss_platform        Up 3 days (healthy)
 mdss_postgres        Up 3 days (healthy)
 mdss_rediscache      Up 3 days (healthy)
 mdssc_api            Up 25 minutes (healthy)  debug until 14:35
 mdssc_binaries       Up 3 days
 mdssc_containers     Up 2 hours               restarts: 2; killed: out of memory
 mdssc_frontend       Up 3 days
 mdssc_notifications  Up 3 days
 mdssc_pgmigrations   Exited (0) 3 days ago
 mdssc_processing     Up 3 days
 mdssc_sourcecode     Up 3 days

 DISK                           USED  AVAILABLE NOTE
 /                               42%        58G
 /var/lib/docker                 91%       9.1G above 90% used

 Run 'mdssc -c status' for the full readiness check.
```

What to look for:

- A service that is not `Up`. `mdssc_pgmigrations` is the exception: it applies the database migrations and then stops with `Exited (0)`.
- `restarts: <n>` in the NOTE column. The service stopped and Docker started it again.
- `killed: out of memory` in the NOTE column. The host does not have sufficient memory for the load.
- `above 90% used` for a disk.
- `debug until HH:MM`. Debug logs are on for the service. See step 6.

#### 2. Image versions

```bash
sudo mdssc version
```

Shows the expected image and the running image of each service. A note marks a service whose running image differs from the expected one, a tag that is not a release, and a tag that `customer.env` overrides, with its line number.

Example output:

```text
 MetaDefender Software Supply Chain 4.3.0 (build sha: 3f9c2e1)

 SERVICE              EXPECTED                                       RUNNING                                        NOTE
 mdssc_pgmigrations   opswat/mdssc_pgmigrations:4.3.0                opswat/mdssc_pgmigrations:4.3.0 (exited)
 mdssc_frontend       opswat/mdssc_frontend:4.3.0                    opswat/mdssc_frontend:4.3.0
 mdssc_api            opswat/mdssc_api:4.3.0-hotfix1                 opswat/mdssc_api:4.3.0-hotfix1                 not a release; set in customer.env:12
 mdssc_sourcecode     opswat/mdssc_sourcecode:4.3.0                  opswat/mdssc_sourcecode:4.3.0
 mdssc_binaries       opswat/mdssc_binaries:4.3.0                    opswat/mdssc_binaries:4.3.0
 mdssc_containers     opswat/mdssc_containers:4.3.0                  opswat/mdssc_containers:4.3.0
 mdssc_notifications  opswat/mdssc_notifications:4.3.0               opswat/mdssc_notifications:4.3.0
 mdssc_processing     opswat/mdssc_processing:4.3.0                  opswat/mdssc_processing:4.3.0
 mdss_postgres        postgres:17                                    postgres:17
 mdcs_rabbitmq        rabbitmq:4.2.4-alpine                          rabbitmq:4.2.4-alpine
 mdss_rediscache      redis:8.6.0-alpine                             redis:8.6.0-alpine
 mdss_platform        opswat/mdcloudservices_mdplatform:2.7.2-mdssc  opswat/mdcloudservices_mdplatform:2.7.2-mdssc  not a release
```

What to look for:

- `differs from expected`. The container runs an image other than the installed version. This can occur after an update that did not complete.
- `set in customer.env:<line>`. A line in `customer.env` overrides the image tag, for example for a hotfix. Make sure that the override is still necessary.
- `not a release`. The tag is not a release version. In version 4.3.0, the `mdss_platform` image always shows this note. You can ignore it for `mdss_platform`.

#### 3. Support report

```bash
sudo mdssc support
```

Prints the status, the versions, the database size, the RabbitMQ queues (the total and the 10 fullest queues) and the number of errors per service in the last 24 hours. Secrets are masked, so you can paste the output into a support ticket. Start with this command.

Example output, after the status and version sections shown in steps 1 and 2:

```text
 DATABASE
   size: 2140 MB

 QUEUES
   1873 messages in 64 queues
       1840  enumerate_storage_content_sourcecode
         33  enumerate_storage_content_containers

 ERRORS IN THE LAST 24 H
   mdcs_jobdispatcher           0
   mdcs_licensingservice        0
   mdcs_scanningservice         12
   mdss_identityservice         1
```

What to look for:

- A queue with many messages. Run the command again after some minutes. If the number does not go down, the service that reads the queue does not process messages.
- A service with errors. Collect the logs of that service with step 4.

#### 4. Recent logs

```bash
sudo mdssc support logs
sudo mdssc support logs --since 6h
sudo mdssc support logs --since 2h --service api
```

- `--since` sets the time window, for example `30m`, `6h` or `2d`. The default is `24h`.
- `--service` keeps only the services whose name contains the value.

The archive holds the container logs, the service log files, `.env`, `customer.env` and `appsettings.json`. Passwords, keys, tokens and connection-string passwords are masked. Only root can read the archive. The command stops if the disk does not have about twice the size of the logs free.

Example output:

```text
Support logs (last 2h, service api) written to /etc/mdssc/support_logs_2026-11-10_12-05-12.tar.gz (3.4M).
```

If the disk is too full, the command stops with a message like this:

```text
Not enough free space in /etc/mdssc: need about 1840 MB, have 950 MB.
```

#### 5. Full support package

```bash
sudo mdssc support full
```

This command is the same as `sudo mdssc -u support_package`. The package holds the logs, host information, product settings, the environment files, and the state of RabbitMQ queues, PostgreSQL tables and Redis keys. The default size limit is 5 GB.

```bash
sudo mdssc -u support_package -m 500M
sudo mdssc -u support_package -s
```

- `-m` sets a smaller size limit, for example `500M` or `1G`.
- `-s` skips the Redis key dump.

The last line of the output shows where the package is:

```text
2026-11-10 12:07:40 UTC [ announce] Support package was exported to /etc/mdssc/mdssc_4.3.0_support_package_2026-11-10_12-07-40.tar
```

The environment files in the package are not masked. Send the package through a secure channel.

If the export fails because the logs are too large, set a lower `LOGS_PER_SERVICE` value in `customer.env` (default `14`), or use `-m`. No restart is necessary.

#### 6. Debug logs

```bash
sudo mdssc debug api --for 30m
sudo mdssc support logs --since 1h --service api
sudo mdssc debug off
```

1. Turn on debug logs for one service. `--for` accepts values such as `30s`, `30m`, `2h` or `1d`. The default is `1h`.
2. Reproduce the problem.
3. Collect the logs of that service.
4. Turn debug logs off, or let them turn off by themselves when the time ends.

You can turn on debug logs for `api`, `sourcecode`, `binaries`, `containers`, `notifications` and `processing`. Platform services are not included. The command recreates the service container, so the service stops for a short time. While debug logs are on, `mdssc status` shows "debug until HH:MM" for the service.

Example output of `sudo mdssc debug api --for 30m`:

```text
Debug logs on for api for 30m. Recreating mdssc_api...
```

Example output of `sudo mdssc debug off`:

```text
Debug logs off for: api. Recreating...
```

#### 7. Quick error scan

```bash
sudo mdssc -u peek_todays_logs
sudo mdssc -u peek_logs
```

`peek_todays_logs` scans today's logs for problems. `peek_logs` scans all logs.

#### Older commands

These commands still work:

```bash
sudo mdssc -u support_package
sudo mdssc -u export_logs
sudo mdssc -u export_info
```

`-u export_logs` is the same as `mdssc logs`. `-u export_info` collects host information. In addition, we offer the option to export your database if you need to use it for migration or debugging purposes. See [PostgreSQL advanced setup](https://www.opswat.com/docs/supply-chain/installation/advanced-installation-for-unix-based-deployments#postgresql-advanced-setup).

### Installation issues

In order to troubleshoot please run LOG_LEVEL=7 [command] where command is the command that has an issue. For example, if MetaDefender Software Supply Chain cannot be started please run the following command:

```bash
sudo LOG_LEVEL=7 mdssc -c start
```

To check the containers and the disk after a start, run `sudo mdssc status`.

### Unable to remove the network

If you encounter some message regarding your network ( similar to network mdssc_stack id xxx has active endpoints ) while you tried to remove or update MDSSC, please try to restart docker:

```bash
systemctl restart docker
```

### "Permission denied" while uninstalling

On some Linux distributions that have SELinux enabled by default you may encounter a "Permission denied" message when uninstalling MDSSC. The uninstall still completes successfully and only some docker containers might still be left running if `mdssc -u clean`  was not executed before the uninstall. This is due to SELinux policies and can be avoided by disabling SELinux temporarily before uninstalling by running:

```bash
sudo setenforce 0
```

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
