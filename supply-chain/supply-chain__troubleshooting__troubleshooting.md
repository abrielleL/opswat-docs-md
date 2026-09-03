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

### Generating support package

In order to generate a support package you can run the next command:

```bash
sudo mdssc -u support_package
```

For more advanced users we offer the following commands:

```bash
sudo mdssc -u export_logs
```

This will allow you to save the logs of the containers.

```bash
sudo mdssc -u export_info
```

This will run some testes and gather info about your system.

```bash
sudo mdssc -u export_settings
```

<p>This command will save the relevant setting from your MDSSC instance.</p>
<p>The archives will be created in <em>/etc/mdssc/</em></p>
<p>In addition, we offer the option to export your database if you need to use it for migration or debugging purposes.</p>

### Installation issues

In order to troubleshoot please run LOG_LEVEL=7 [command] where command is the command that has an issue. For example, if MetaDefender Software Supply Chain cannot be started please run the following command:

```bash
sudo LOG_LEVEL=7 mdssc -c start
```

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
