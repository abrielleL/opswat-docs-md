<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/why-does-a-report-fail-to-load-with-error--api-took-too-long-to- -->

# Why does a report fail to load with error "API took too long to respond"?

This article applies to all MDSS versions

> When opening a report in MDSS, the UI displays the following error:

`API took too long to respond. Please try again later`

The database queries are taking more than 60 seconds to return, triggering the default web server (nginx) timeout.

Increase the **nginx proxy timeout** and **PostgreSQL query timeout** values.

Both changes are required.

### [**For Windows**](/docs/mdss/knowledge-base/why-does-a-report-fail-to-load-with-error--api-took-too-long-to-#for-windows)

1. Stop MDSS services
2. Increase Nginx Timeout Create a backup of the nginx configuration file at `C:\Program Files\OPSWAT\MetaDefender Storage Security\webclient\default.conf`, then edit the **default.conf** file Add or modify the following values in the appropriate `location` or `http` block:

proxy_connect_timeout 300s;
proxy_send_timeout 300s;
proxy_read_timeout 300s;

3. Increase PostgreSQL Timeout Edit the MDSS environment configuration file at `C:\Program Files\OPSWAT\MetaDefender Storage Security\config\customer.env` Modify the `POSTGRESQL_URL` parameter to include increased timeout values. Example:

POSTGRESQL_URL=Host=postgres;Port=5432;Username=mdss;Password=<password>;Database=MDSS;Timeout=300;CommandTimeout=300

4. Start MDSS services

### [F**or Linux**](/docs/mdss/knowledge-base/why-does-a-report-fail-to-load-with-error--api-took-too-long-to-#for-linux)

1. Stop MDSS service

sudo mdss -c stop

2. Increase Nginx Timeout Run the bellow command

sudo awk '/proxy_intercept_errors off;/{print; print " proxy_connect_timeout 300s;"; print " proxy_send_timeout 300s;"; print " proxy_read_timeout 300s;"; next}1' /etc/mdss/webclient/default.conf | sudo tee /etc/mdss/webclient/default.conf.tmp && sudo mv /etc/mdss/webclient/default.conf.tmp /etc/mdss/webclient/default.conf

This will create a backup of the config file `/etc/mdss/webclient/default.conf`and increase the nginx timeout to 300ms

3. Increase the timeout for the PostgreSQL database by modifying the `POSTGRESQL_URL` in the `/etc/mdss/customer.env` file:

   - Set `Timeout` to 300.
   - Set `CommandTimeout` to 300.

Here's an example of how the `POSTGRESQL_URL` should look:

POSTGRESQL_URL=Host=postgres;Port=5432;Username=mdss;Password=a3ZPzF1VIN3RzCu5YWrl;Database=MDSS;Timeout=300;CommandTimeout=300

4. Start MDSS service

sudo mdss -c startNote

- Increasing the timeout allows **long-running report queries** to complete successfully.
- If the issue occurs frequently, it may indicate:

  - very large report datasets
  - insufficient database resources
  - missing database indexes

In those cases, further **database performance tuning** may be required.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
