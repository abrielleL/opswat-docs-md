<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta -->

# How to Configure MetaDefender Core Syslog to an AWS Ubuntu Instance

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems from version v5.15.1 and newer

## [📘 Overview](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#-overview)

This article provides step-by-step instructions to configure a cloud-hosted Ubuntu instance on Amazon Web Services (AWS) as a Syslog receiver and connect it to MetaDefender Core via the Management Console.

### [Prerequisites](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#prerequisites)

- **AWS Console Access:** Permissions to modify EC2 Security Groups.
- **Ubuntu EC2 Instance:** Root or `sudo` SSH access to the target Linux server.
- **MetaDefender Core:** Administrator access to the Management Console.

## [🛠️ Step-by-Step Instructions](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#-step-by-step-instructions)

### [Phase 1: Configure AWS Infrastructure (Security Groups)](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#phase-1-configure-aws-infrastructure-security-groups)

By default, AWS blocks all inbound traffic. You must explicitly allow Syslog traffic (Port 514) to reach your Ubuntu instance.

1. Log in to the **AWS Management Console** and navigate to the **EC2 Dashboard**.
2. Select your Ubuntu instance and locate the **Security** tab at the bottom of the screen. Click on the associated **Security Group** link.
3. Click **Edit inbound rules**.
4. Click **Add rule** and configure the following:

   - **Type:** Custom UDP Rule (and/or Custom TCP Rule depending on your preference).
   - **Port Range:** `514`
   - **Source:** Select `Custom` and input the public IP address (or Private VPC IP, if peered) of your MetaDefender Core server.

**💡 Pro Tip:** Add `/32` to the end of the IP to restrict access strictly to the Core server (e.g., `198.51.100.20/32`).

5. Click **Save rules**.

### [Phase 2: Configure the Ubuntu Instance (`rsyslog`)](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#phase-2-configure-the-ubuntu-instance-rsyslog)

Ubuntu uses `rsyslog` as its default logging service, but it only accepts internal logs out-of-the-box. You must configure it to listen for external connections.

1. Connect to your AWS Ubuntu instance via SSH.
2. Open the `rsyslog` configuration file using a text editor (e.g., `nano`):

sudo nano /etc/rsyslog.conf

1. Scroll down to the `MODULES` section. Uncomment the following lines (remove the `#` at the beginning) to enable UDP and/or TCP reception:

**For UDP (Standard Syslog):**

module(load="imudp")
input(type="imudp" port="514")

**For TCP (Reliable Syslog):**

module(load="imtcp")
input(type="imtcp" port="514")

4. Save the file and exit (`Ctrl+O`, `Enter`, `Ctrl+X` in nano).
5. Restart the `rsyslog` service to apply the changes:

sudo systemctl restart rsyslog

6. Check for the rsyslog service status and make sure its showing active and running

sudo systemctl status rsyslog"

7. Verify the service is actively listening on port 514:

sudo ss -tuln | grep 514

### [Phase 3: Configure MetaDefender Core](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#phase-3-configure-metadefender-core)

Now that the AWS server is ready to receive data, configure MetaDefender Core to forward the logs.

1. Log in to the **MetaDefender Core Management Console**.
2. Navigate to **Settings** > **Logs >> Edit**.
3. Under **Syslog** tab >> **Add a connection**
4. Input the details for your AWS Ubuntu instance in **{protocol}://{ip address}:{port}** format

   - **Server Address:** The Public IP address (or Private IP if internally routed) of your AWS EC2 instance.
   - **Port:** `514`
   - **Protocol:** `UDP` (or `TCP` if configured in Phase 2).
5. Click on **Save Changes**to save the configuration.

### [Phase 4: Verification](/docs/mdcore/v5.21.0/knowledge-base/how-to-configure-metadefender-core-syslog-to-an-aws-ubuntu-insta#phase-4-verification)

To confirm that logs are successfully travelling from MetaDefender Core to your AWS instance:

1. Return to your SSH session on the Ubuntu instance.
2. Run the following command to watch the live incoming system logs:

sudo tail -f /var/log/syslog

1. Trigger an event in MetaDefender Core (e.g., upload a file for scanning, or log out and log back into the UI).
2. Watch the Ubuntu terminal. You should see new log entries appear containing the `ometascan` or `mdcore` service tags.

Troubleshooting Note:

If logs do not appear, verify that the Ubuntu Uncomplicated Firewall (UFW) is not overriding the AWS Security Group. You can check this by running `sudo ufw status`. If active, run `sudo ufw allow 514/udp`.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
