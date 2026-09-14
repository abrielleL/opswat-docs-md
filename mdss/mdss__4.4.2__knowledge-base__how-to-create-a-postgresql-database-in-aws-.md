<!-- source: https://www.opswat.com/docs/mdss/4.4.2/knowledge-base/how-to-create-a-postgresql-database-in-aws- -->

# How to create a PostgreSQL Database in AWS?

Affected product: MDSS 4.0.0 and newer

Overview:

MetaDefender Storage Security (MDSS) requires a PostgreSQL database to store configuration data, scan results, and operational metadata. This guide walks administrators through the complete process of provisioning a PostgreSQL instance on AWS (using Aurora or RDS), configuring the required database and permissions, and establishing the connection with MDSS.

Prerequisites

• An active AWS account with permissions to create RDS or Aurora PostgreSQL instances.

• Access to the target PostgreSQL server via pgAdmin or psql.

• MDSS 4.0.0 or newer installed, with access to its configuration files (customer.env).

• Network connectivity between the MDSS host and the AWS RDS/Aurora endpoint (security groups and firewall rules must allow traffic on port 5432).

Steps to configure:

1. Create the PostgreSQL instance in AWS

In AWS, search for Aurora and RDS.

Select Create and choose full configuration.

Figure 1. Select PostgreSQL in Aurora/RDS and use full configuration.

After the instance is created, open the database details and copy the endpoint. This will be the PostgreSQL host. The default port is 5432. If the port has been changed, copy that value as well.

Figure 2. Copy the endpoint and confirm the database port.

2. Create the MDSS database and assign permissions

Option A: Using pgAdmin

In pgAdmin, connect to the target PostgreSQL server.

Right-click Databases, then select Create > Database....

Figure 3. Create a new database from pgAdmin.

On the General tab, enter “mdss” as the database name. On the Security tab, assign the required privileges to the target user, then click Save.

Figure 4. Set the database name to mdss.

Figure 5. Apply the required permissions and save the database.

Option B: Using psql

Use the following commands to connect, create the database, and grant the required permissions.

psql -h db.example.com -p 5432 -U myuser
-- 1. Create database
CREATE DATABASE mdss;
-- 2. Database connection
GRANT CONNECT ON DATABASE mdss TO myuser;
 -- 3. Schema permissions
GRANT CREATE, USAGE ON SCHEMA public TO myuser;
 -- 4. Full privileges on existing objects
GRANT ALL PRIVILEGES ON ALL TABLES IN SCHEMA public TO myuser;
GRANT ALL PRIVILEGES ON ALL SEQUENCES IN SCHEMA public TO myuser;
GRANT ALL PRIVILEGES ON ALL FUNCTIONS IN SCHEMA public TO myuser;
GRANT ALL PRIVILEGES ON ALL PROCEDURES IN SCHEMA public TO myuser;
 -- 5. Default privileges for new objects
ALTER DEFAULT PRIVILEGES IN SCHEMA public 
GRANT ALL PRIVILEGES ON TABLES TO myuser;
ALTER DEFAULT PRIVILEGES IN SCHEMA public 
GRANT ALL PRIVILEGES ON SEQUENCES TO myuser;
ALTER DEFAULT PRIVILEGES IN SCHEMA public 
GRANT ALL PRIVILEGES ON FUNCTIONS TO myuser;
 -- 6. For encryption extensions (if needed)
GRANT USAGE ON SCHEMA pg_catalog TO myuser;

3. Configure the new PostgreSQL server in MDSS

Add the connection details to customer.env.

POSTGRES_USER=user
POSTGRES_PASSWORD=password
POSTGRES_DB=mdss
POSTGRESQL_URL=Host=postgres;Port=5432;Username=user;Password=password;Database=mdss

Save the file and start the MDSS service.

Verify functionality:

Once the MDSS service has started, use the following checks to confirm that the database connection is working correctly.

1. Check the database connection directly from the MDSS server

From the MDSS host or any machine with network access to the RDS/Aurora endpoint, run the following command to verify that the database is reachable and the credentials are valid:

psql -h <POSTGRES_HOST> -p 5432 -U <POSTGRES_USER> -d mdss -c "\conninfo"

A successful response will display the connection details, confirming that the user, host, port, and database are all correct. If the connection fails, verify that the endpoint, credentials, and AWS security group rules are configured correctly.

2. Verify the MDSS web interface

Open a browser and navigate to the MDSS management interface. If the database connection is healthy, you will see the user configuration wizard. Any database connectivity issues will typically surface as a page showing errors connecting to the database.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
