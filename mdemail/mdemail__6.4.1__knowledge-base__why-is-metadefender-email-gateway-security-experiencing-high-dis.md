<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/knowledge-base/why-is-metadefender-email-gateway-security-experiencing-high-dis -->

# Why is MetaDefender Email Gateway Security Experiencing High Disk Usage?

**Check Your Version:** This article applies to MetaDefender Email Gateway Security version 6.1.1 releases deployed on Windows systems.

### [**Issue:**](/docs/mdemail/6.4.1/knowledge-base/why-is-metadefender-email-gateway-security-experiencing-high-dis#issue)

Users may observe high disk usage on systems running MetaDefender Email Gateway Security version 6.1.1. This is typically due to the underlying PostgreSQL database growing in size over time. Even after performing cleanup operations through the UI (such as deleting scanned emails or attachments), the disk space may not be immediately recovered. This is because PostgreSQL retains obsolete data (known as dead tuples) until a VACUUM operation is executed.

### [**Resolution:**](/docs/mdemail/6.4.1/knowledge-base/why-is-metadefender-email-gateway-security-experiencing-high-dis#resolution)

Follow the steps below to run the VACUUM operation manually:

**Steps:**

1. **Open Command Prompt as Administrator**

   - Click **Start**, type `cmd`, right-click **Command Prompt**, and select **Run as Administrator**.
2. **Navigate to PostgreSQL Installation Directory**

   cd "C:\Program Files\OPSWAT\MetaDefender Email Security\postgre\bin"
   - Note: Update the path if PostgreSQL is installed in a different location.
3. **Execute the VACUUM Command**

   - Use the `psql` tool to connect to the PostgreSQL database and run the VACUUM operation:psql -h localhost -p <port> -U <username> -d mdemailsecurity -W -c "VACUUM"
   - Replace the following placeholders as needed:

     - `<port>`: Default PostgreSQL port (e.g., 5432)
     - `<username>`: PostgreSQL database user (e.g., postgres)

### [**Prevention:**](/docs/mdemail/6.4.1/knowledge-base/why-is-metadefender-email-gateway-security-experiencing-high-dis#prevention)

To ensure consistent performance and disk space management, consider scheduling this command using Windows Task Scheduler to run at defined intervals (e.g., weekly or bi-weekly).

**Support:** If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
