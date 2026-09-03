<!-- source: https://www.opswat.com/docs/filescan/3.1.1/installation/installation-options -->

# Installation Options

Before starting the installation process, you can modify certain installation options in the `install.cfg` file that is located in the same folder as `install.sh`.

Warning

The **default installation options are perfectly suitable** for most use cases, so it is not recommended to change these values unless you have a special use case.

**Step #1 - Open** `install.cfg` **in a text editor**

Warning

For **upgrade installations**, the installation options should be changed in `/home/sandbox/sandbox/install.cfg` (or in the custom Sandbox_Directory that you configured previously).

**Step #2 - Change the installation options by modifying the following properties:**

install.cfgCopySandbox_User="sandbox"
Sandbox_Directory="/home/sandbox/sandbox"
Sandbox_ConfigureFirewall=true
Sandbox_OverwriteDockerDaemonJson=true
Sandbox_UseCommunityYaraRules=false
SandboxTransform_Install=true
SandboxTransform_APIKeySecret=
SandboxBroker_Install=true
SandboxBroker_APIKeySecret=
SandboxWebservice_Install=true
SandboxWebservice_Engine_Host=
SandboxWebservice_Engine_Secret=

**Step #3 - Save the modified file and start the installation process**

## [Property details](/docs/filescan/3.1.1/installation/installation-options#property-details)

| Property Name | Default Value | Description |
| --- | --- | --- |
| Sandbox_User | sandbox | Defines the user that will run the Sandbox service. This user will be created automatically by the installer if it does not exist. For security reasons, this user should not have a password or sudo access! |
| Sandbox_Directory | /home/sandbox/sandbox | The directory where Sandbox will be installed. It must be within the home directory of the Sandbox_User. |
| Sandbox_ConfigureFirewall | true | If set to true, the installer configures the necessary firewall rules using iptables-persistent. Most importantly, it opens port 443. |
| Sandbox_OverwriteDockerDaemonJson | true | If set to true, the installer overwrites the existing /etc/docker/daemon.json configuration file. Set this to false if you have any custom modifications in that file. |
| Sandbox_UseCommunityYaraRules | false | If set to true, the installer will clone GitHub repositories containing the latest YARA rules provided by the Malware Analysis community (these repositories are not controlled by OPSWAT). More details at [YARA Rules](/docs/filescan/3.1.1/configuration/yara-rules). |
| SandboxTransform_Install | true | If set to true, the "transform" component of Sandbox will be installed. |
| SandboxTransform_APIKeySecret |  | Specifies the internal API key used by transform. If left blank, a random API key will be generated. |
| SandboxBroker_Install | true | If set to true, the "broker" component of Sandbox will be installed. |
| SandboxBroker_APIKeySecret |  | Specifies the internal API key used by broker. If left blank, a random API key will be generated. |
| SandboxWebservice_Install | true | If set to true, the "webservice" component of Sandbox will be installed. |
| SandboxWebservice_Engine_Host |  | Specifies the address where the webservice can connect to the broker. If left blank, it will be automatically set to "broker". |
| SandboxWebservice_Engine_Secret |  | Specifies the internal API key used by webservice to connect to broker. If left blank, it will be set to SandboxBroker_APIKeySecret. |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
