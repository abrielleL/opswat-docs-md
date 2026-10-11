<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/portable-package-known-issue-in-451 -->

# Portable package and offline docker toolkit are not starting due to RabbitMQ deprecated feature not being permitted?

After deploying MetaDefender Storage Security from the **portable package** or the **offline Docker toolkit**, the product does not become available. The `mdcs_rabbitmq` container is running, but the backend containers (licensing service, API gateway and the other services) restart continuously.

Service logs contain repeated entries similar to:

```bash
[Fatal] : (EventBusLibrary) RabbitMq subscribeChannel has been closed unexpectedly
(ReplyCode: 541, ReplyText: INTERNAL_ERROR - Feature `transient_nonexcl_queues` is deprecated.
By default, this feature is not permitted anymore.)
```

Messages such as `nc: bad address 'licensingservice'` or `Error loading shared library libgssapi_krb5.so.2` may also appear. These are side effects of the restart loop, not the cause.

### Affected deployments:

| **Versions** | 4.5.0 and 4.5.1 |

| **Affected** | Portable package, offline Docker toolkit |

| **Not affected** | Deployments made with the Linux (RPM/DEB) or Windows installers |

### **Confirming the issue**

Run the following in your MDSS deployment directory:

```bash
ls -la ./rabbitmq/
```

If `rabbitmq.conf` is listed as a directory (a `d` at the start of the permissions column) instead of a regular file, this issue applies to your deployment.

You can confirm it a second way:

```bash
docker exec mdcs_rabbitmq rabbitmqctl eval 'rabbit_deprecated_features:is_permitted(transient_nonexcl_queues).'
```

A healthy deployment returns `true`. An affected deployment returns `false`.

### Solution:

Run these commands in your MDSS deployment directory:

```bash
sudo rm -r ./rabbitmq/rabbitmq.conf
echo 'deprecated_features.permit.transient_nonexcl_queues = true' | sudo tee ./rabbitmq/rabbitmq.conf
sudo chmod 704 ./rabbitmq/rabbitmq.conf
sudo ./mdss.sh -c restart
```

The services reconnect automatically once RabbitMQ restarts. Verify the result with:

```bash
docker exec mdcs_rabbitmq rabbitmqctl eval 'rabbit_deprecated_features:is_permitted(transient_nonexcl_queues).'
```

The command must now return `true`, and the service containers must stop restarting.

> The missing file is included in the packages starting with version **4.5.2**. New deployments made from 4.5.2 or later are not affected.

> **When upgrading an affected deployment,** apply the `rm -r` step above at least once. As long as `rabbitmq.conf` exists as a directory, neither unpacking a newer package nor running an update can replace it with the correct file, and the deployment remains affected after the upgrade.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
