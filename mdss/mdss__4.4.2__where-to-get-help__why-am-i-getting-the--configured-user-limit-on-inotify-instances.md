<!-- source: https://www.opswat.com/docs/mdss/4.4.2/where-to-get-help/why-am-i-getting-the--configured-user-limit-on-inotify-instances -->

# Why am I getting the 'Configured user limit on inotify instances has been reached' error in MDSS on Linux/Kubernetes?

Linux uses **inotify** to monitor file system events, but it enforces limits on how many files and directories a single user can watch. The default limits (often **128 instances** and **8,192 watches**) are too low for Kubernetes workloads. You will need to raise this value higher to run MDSS.

Please Note:

If using a **cloud-managed cluster** (e.g., GKE, EKS, AKS), nodes are preconfigured, and changes may not be necessary or possible. Ensure this setting is adjusted on **all Kubernetes nodes** if needed.

Sample Error Log:

LogCopy[2025-03-27 08:02:01Z] [Fatal] : Unable to start Discovery service │
System.IO.IOException: The configured user limit (128) on the number of inotify instances has been reached, or the per-process limit on the number of open file descriptors has been reached. │
at System.IO.FileSystemWatcher.StartRaisingEvents() │
at Microsoft.Extensions.FileProviders.Physical.PhysicalFilesWatcher.TryEnableFileSystemWatcher() │
at Microsoft.Extensions.FileProviders.Physical.PhysicalFilesWatcher.CreateFileChangeToken(String filter) │
at Microsoft.Extensions.Primitives.ChangeToken.ChangeTokenRegistration`1..ctor(Func`1 changeTokenProducer, Action`1 changeTokenConsumer, TState state) │
at Microsoft.Extensions.Primitives.ChangeToken.OnChange(Func`1 changeTokenProducer, Action changeTokenConsumer) │
at Microsoft.Extensions.Configuration.FileConfigurationProvider..ctor(FileConfigurationSource source) │
at Microsoft.Extensions.Configuration.Json.JsonConfigurationSource.Build(IConfigurationBuilder builder) │
at Microsoft.Extensions.Configuration.ConfigurationBuilder.Build() │
at Microsoft.Extensions.Hosting.HostBuilder.InitializeAppConfiguration() │
at Microsoft.Extensions.Hosting.HostBuilder.Build() │
at opswat.mdss.discovery.service.Program.Main(String[] args) in /app/Backend/src/Discovery/opswat.mdss.discovery.service/Program.cs:line 27

You can check your current inotify instances of your nodes by running these commands:

BashCopysysctl fs.inotify.max_user_instances
sysctl fs.inotify.max_user_watches

### [**Solution:**](/docs/mdss/4.4.2/where-to-get-help/why-am-i-getting-the--configured-user-limit-on-inotify-instances#solution)

1. To immediately raise the limits without restarting, run:

BashCopysudo sysctl -w fs.inotify.max_user_instances=8192
sudo sysctl -w fs.inotify.max_user_watches=1048576

This takes effect immediately but will reset after a reboot. You can modify the values to be higher based on your needs.

2. To ensure these limits remain after a restart, add them to the system configuration file:

BashCopyecho "fs.inotify.max_user_instances=8192" | sudo tee -a /etc/sysctl.conf
echo "fs.inotify.max_user_watches=1048576" | sudo tee -a /etc/sysctl.conf

3. Once updated, apply the new settings by running:

BashCopysudo sysctl -pSupport:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
