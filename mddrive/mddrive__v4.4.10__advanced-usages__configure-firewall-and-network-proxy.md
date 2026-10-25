<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/advanced-usages/configure-firewall-and-network-proxy -->

# Configure Firewall and Network Proxy

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Depending on organizations' policies, MetaDefender Drive might fail to connect to OPSWAT Central Management or to download updates using MetaDefender Drive Toolkit due to firewall or network proxy configuration. In case of such connection failure, specific hosts must be allowed by the firewall, and proxy settings might need to be configured accordingly.

## [Hosts to Allow](/docs/mddrive/v4.4.10/advanced-usages/configure-firewall-and-network-proxy#hosts-to-allow)

Your network admin must allow access to the following hosts for MetaDefender Drive and MetaDefender Drive Toolkit to work:

| **Host** | **Function** |
| --- | --- |
| [**https://activation.dl.opswat.com**](https://activation.dl.opswat.com/) | To activate licenses online |
| [**https://update.dl.opswat.com**](https://update.dl.opswat.com/) | To download scanning engine updates |
| [**https://installer-cdn.opswat.com/MD_Drive_Toolkit/3.0/update_infra/main/**](https://installer-cdn.opswat.com/MD_Drive_Toolkit/3.0/update_infra/main/MetaDefenderDriveToolkit.zip) | To download MetaDefender Drive Toolkit’s new version |
| [**https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/**](https://installer-cdn.opswat.com/MD_Drive/3.0/update_infra/main/) | To download MetaDefender Drive’s new software releases |

## [Editing Network Proxy](/docs/mddrive/v4.4.10/advanced-usages/configure-firewall-and-network-proxy#editing-network-proxy)

The following are the steps to follow on a Linux operating system to configure network proxy:

1. Open the system settings.
2. Navigate to the **Network** settings from the left pane or use the search function.
3. Click the **Gear Icon** in the Network Proxy section.
4. Select the **Manual** option.
5. Enter the proxy server details as instructed by your organization’s IT specialists.

Network Proxy settings on Linux
