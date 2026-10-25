<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/integrations/wallix-bastion -->

# Wallix Bastion

View as Markdown Ask ChatGPT about this page Ask Claude about this page Warning

Wallix only supports AV multi-scanning. It does not accept Sanitized/Redacted content in the response (e.g. from CDR or redact feature of DLP).

**Important**: The default scan timeout for Wallix Bastion is 10 seconds for SCP and 20 seconds for copy file over RDP. If this timeout needs to be adjusted to handle large and complex files, please refer to [How to increase the scan timeout](/docs/mdicap/v5.15.0/integrations/wallix-bastion#how-to-increase-the-scan-timeout) to adjust this value

Note: This document was made base on Wallix Bastion v12.0.9

## [Integration With MD ICAP Server](/docs/mdicap/v5.15.0/integrations/wallix-bastion#integration-with-md-icap-server)

## [RDP](/docs/mdicap/v5.15.0/integrations/wallix-bastion#rdp)

### [Configure the MD ICAP Server as AV Scan for RDP](/docs/mdicap/v5.15.0/integrations/wallix-bastion#configure-the-md-icap-server-as-av-scan-for-rdp)

**Step 1**: Go to Configuration -> Configuration Options -> RDP proxy

**Step 2**: input the IP Adress of MD ICAP Server into section "*icap_server_down*" and "*icap_server_up*"

E.g:

- the IP address of MD ICAP Server is 10.40.168.128
- default port of ICAP communication: 1344
- Service name can be set "avscan" as default

### [Enable the AV scan for RDP](/docs/mdicap/v5.15.0/integrations/wallix-bastion#enable-the-av-scan-for-rdp)

**Step 1**: Go to Session Management -> Connection policies -> RDP

**Step 2**: Edit the policy for RDP

**Step 3**: enable all checkboxes in "File_verification" section and hit "Apply" button

## [SSH](/docs/mdicap/v5.15.0/integrations/wallix-bastion#ssh)

### [Configure the MD ICAP Server as AV Scan for SSH](/docs/mdicap/v5.15.0/integrations/wallix-bastion#configure-the-md-icap-server-as-av-scan-for-ssh)

**Step 1**: Go to Configuration -> Configuration Options -> SSH proxy

**Step 2**: Add MD ICAP Server information to 2 sections "icap_server_up" and "icap_server_down"

e.g:

- the IP address of MD ICAP Server is 10.40.168.128
- default port of ICAP communication: 1344
- Service name can be set "avscan" as default

### [Enable the AV scan for SSH](/docs/mdicap/v5.15.0/integrations/wallix-bastion#enable-the-av-scan-for-ssh)

**Step 1**: Go to Session Management -> Connection policies -> SSH

**Step 2**: Edit the policy for RDP

**Step 3**: enable all checkboxes in "File_verification" section and hit "Apply" button

## [How to increase the scan timeout](/docs/mdicap/v5.15.0/integrations/wallix-bastion#how-to-increase-the-scan-timeout)

by default, Wallix Bastion v12.0.9 can not adjust the scan timeout for both RDP and SSH, below deb package need to be downloaded and installed

link to download

BashCopyhttps://cloud.wallix.com/index.php/s/DKsW2qTNNceqiRN

Install as below steps:

BashCopy1. Upload the deb package to the Bastion using SCP/2242
2. Connect to the Bastion with SSH on port 2242
3. Type super sudo -i and enter twice the wabsuper password
4. Type dpkg -i ~wabadmin/python3-wallix-validator_0.7.10_amd64.deb (assuming it uploaded to the default directory ~wabadmin)
### [Adjust scan timeout for RDP](/docs/mdicap/v5.15.0/integrations/wallix-bastion#adjust-scan-timeout-for-rdp)

**Step 1**.Connect to the Bastion with SSH on port 2242

**Step 2**.In the file **/opt/wab/share/conf/rdpproxy.spec**, in the two sections **[icap_server_up]** and **[icap_server_down]**, add:

BashCopy#_advanced
timeout = integer(min=1, max=3000, default=500)

now you are able to configure the timeout from the WEB UI in **Configuration** -> **Configuration options** -> **RDP proxy** (with "Advance Options" checkbox enable)

### [Adjust scan timeout for SSH](/docs/mdicap/v5.15.0/integrations/wallix-bastion#adjust-scan-timeout-for-ssh)

**Step 1**.Connect to the Bastion with SSH on port 2242

**Step 2**.In the file : **/opt/wab/share/conf/sashimi.spec** , in the two sections **[icap_server_up]** and **[icap_server_down]**, add:

BashCopy#_advanced
timeout = integer(min=1, max=3000, default=500)

now you are able to configure the timeout from the WEB UI in **Configuration** -> **Configuration options** -> **SSH proxy** (with "Advance Options" checkbox enable)

**Step 3**.In the file **/opt/wab/share/conf/protocols/ssh.spec** , in the sections **[file_verification]** add:

BashCopy#_advanced
validator_response_timeout = integer(min=5, default=500)

now you are able to configure the timeout from the WEB UI in **Session management** -> **Connection policies**-> **SSH** (with "Advance Options" checkbox enable)
