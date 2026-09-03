<!-- source: https://www.opswat.com/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls -->

# Configure Firewall Rules to Allow Incoming Connections

Some deployments require inbound network access on specific TCP ports. If the operating system firewall blocks these ports, clients or services may be unable to connect.

This guide explains how to allow inbound TCP connections using several commonly used firewall solutions.

## [Windows Defender Firewall](/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls#windows-defender-firewall)

### [Option 1: Using the Windows Defender Firewall Console](/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls#option-1-using-the-windows-defender-firewall-console)

1. Open **Windows Defender Firewall** from the Windows Start menu or search bar.

2. Select **Advanced settings** to open **Windows Defender Firewall with Advanced Security**.

3. Select **Inbound Rules***.*

4. In the **Actions** at the right-hand pane, click **New Rule...**.

5. Select **Port** and click **Next**.

6. Select **TCP**, specify the required port number, and click **Next**.

If you are unsure which protocol or port to use, refer to your application's documentation.

7. Select **Allow the connection**, then click **Next**.

8. Accept the default settings and click **Next**.

9. Enter a descriptive name for the rule (e.g., "Open Port”) and click **Finish**.

### [Option 2: Using PowerShell](/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls#option-2-using-powershell)

1. Run **PowerShell** as **Administrator**.
2. Run the following command, replacing the placeholders with the appropriate values:

PowershellCopyNew-NetFirewallRule `
-DisplayName "<Rule Name>" `
-Direction Inbound `
-Action Allow `
-Protocol TCP `
-LocalPort <Port Number>

---

## [Uncomplicated Firewall (UFW)](/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls#uncomplicated-firewall-ufw)

1. Verify that **UFW** is running.

BashCopysudo ufw status

Expected output:

Status: active

2. Allow a TCP port, replacing the placeholders with the appropriate value.

BashCopysudo ufw allow <your port>/tcp

Example output:

Rule added
Rule added (v6)

3. Verify the firewall rule.

BashCopysudo ufw status

Confirm that the specified port appears in the list of allowed rules.

---

## [Firewalld](/docs/mdcluster/trouble-shooting/how-to-open-a-port-on-common-firewalls#firewalld)

1. Verify that **firewalld** is running:

BashCopysudo firewall-cmd --state

Expected output:

running

2. Allow a TCP port. Add a permanent firewall rule:

BashCopysudo firewall-cmd --permanent --add-port=80/tcp

3. Reload the firewall configuration to apply the change:

JavaScriptPythonCopysudo firewall-cmd --reloadprint("hello")

4. Verify the firewall rule:

BashCopysudo firewall-cmd --list-ports

Confirm that the specified port is included in the list of allowed ports.
