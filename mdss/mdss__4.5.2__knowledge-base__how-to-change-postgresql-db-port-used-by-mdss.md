<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/how-to-change-postgresql-db-port-used-by-mdss -->

# How to change PostgreSQL DB port used by MDSS

Steps

1. Stop MDSS Services

Open Services (services.msc) and stop the following:

- MDSS service
- PostgreSQL service
- Mdss_rabbitmq

2. Edit Configuration
3. Navigate to:

C:\Program Files\OPSWAT\MetaDefender Storage Security\config

2. Open customer.env in a text editor.
3. Update the following parameters:

POSTGRESQL_PORT=<new_port>       # e.g., 5435 POSTGRESQL_URL=jdbc:postgresql://localhost:<new_port>/mdss

4. Save and close the file.
5. Refresh Environment
6. Open PowerShell as Administrator.
7. Run:

cd "C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts" .\mdss.ps1 -c refresh

This refreshes environment variables and restarts MDSS services.

4. Start Services

If not already started, manually start the services stopped in Step 1.

5. Verify

Confirm MDSS is listening on the new port:

netstat -ano | findstr :<new_port>

6. Troubleshooting

- Check MDSS logs:

C:\Program Files\OPSWAT\MetaDefender Storage Security\logs

- Ensure no other application is using the new port.

> **Support:**
>
> If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
