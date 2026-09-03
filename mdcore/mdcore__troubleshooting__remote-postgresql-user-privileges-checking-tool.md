<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/remote-postgresql-user-privileges-checking-tool -->

# Remote PostgreSQL User Privileges Checking Tool

Check out [PostgreSQL User Privilege Requirements](/docs/mdcore/troubleshooting/postgresql-user-privilege-requirement) to learn more all detailed requirements while setting up remote PostgreSQL database server for MetaDefender Core.

This tool is to help your database system admin quickly determine whether or not your remote PostgreSQL database have sufficient user privileges as described at [PostgreSQL User Privilege Requirements](/docs/mdcore/troubleshooting/postgresql-user-privilege-requirement) to work properly with MetaDefender Core application.

Download links:

- **Windows:** <https://metascanbucket.s3.amazonaws.com/Metadefender/Core/utilities/PGComplianceCheck/windows/check-db-user-compliance.exe>
- **CentOS / Red Hat:** <https://metascanbucket.s3.amazonaws.com/Metadefender/Core/utilities/PGComplianceCheck/centos/check-db-user-compliance>
- **Debian / Ubuntu:** <https://metascanbucket.s3.amazonaws.com/Metadefender/Core/utilities/PGComplianceCheck/debian/check-db-user-compliance>

Tool dependencies

Ensure that the tool is executed on a host where the psql executable is present and can be invoked from the command line.

**Usage:**

BashCopycheck-db-user-compliance -h <HOSTNAME> -p <PORT> -u <DATABASE USER> -m <MAIN USER NEED TO CHECK> -i <INTERNAL USER NEED TO CHECK>

**Options and arguments:**

- -h (--help) instruction
- -h (--hostname) database server host or socket directory
- -p (--port) database server port
- -u (--pguser) database user name
- -m (--mainuser) PostgreSQL main user
- -i (--internaluser) PostgreSQL internal user

Set environmental path

If the PostgreSQL own `psql` executable file has not been assigned to the Windows environmental path yet, and PostgreSQL's registry value does not exist, user has to input their own psql executable path.

**Examples:**

**A. Inspecting PostgreSQL main user**

Example 1: PostgreSQL main user with SUPERUSER privilege

BashCopycheck-db-user-compliance -h 172.168.1.196 -p 54321 -u postgres -m postgres
==== COMPLIANT RESULTS ====
Validating main user...
Main PostgreSQL user: OK

Example 2: PostgreSQL main user with CREATEDB and CREATEROLE privilege

BashCopycheck-db-user-compliance -h 172.168.1.196 -p 54321 -u postgres -m mdcore
==== COMPLIANT RESULTS ====
Validating main user...
Main PostgreSQL user: OK
WARNINGS:
- Your user doesn't have SUPERUSERTRUE privilege
- MetaDefender Core could not be upgraded from standalone to share mode
- MetaDefender Core could not drop the default generated internal users usr_xxxxxxx

Example 3: PostgreSQL main user without privilege

BashCopycheck-db-user-compliance -h 172.168.1.196 -p 54321 -u postgres -m test
==== COMPLIANT RESULTS ====
Validating main user...
Main PostgreSQL user: FAILED
WARNINGS: Your user doesn't have SUPERUSER privilege

**B. Inspecting PostgreSQL internal user**

Example 1: PostgreSQL internal user with LOGIN privilege

BashCopycheck-db-user-compliance -h 172.168.1.196 -p 54321 -u postgres -m postgres -i usr_8f013d25006fe9431ec198ad7af7c6aa3ef7f65b
==== COMPLIANT RESULTS ====
Validating main user...
Main PostgreSQL user: OK
Validating internal user...
Internal PostgreSQL user: OK

Example 2: PostgreSQL internal user without LOGIN privilege

check-db-user-compliance -h 172.168.1.196 -p 54321 -u postgres -m postgres -i test
==== COMPLIANT RESULTS ====
Validating main user...
Main PostgreSQL user: OK
Validating internal user...
Internal PostgreSQL user: FAILED
WARNINGS: Your user doesn't have LOGINTRUE privilege
