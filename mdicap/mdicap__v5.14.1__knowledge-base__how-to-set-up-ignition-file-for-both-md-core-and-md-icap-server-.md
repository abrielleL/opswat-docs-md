<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/how-to-set-up-ignition-file-for-both-md-core-and-md-icap-server- -->

# How to set up ignition file for both MD Core and MD ICAP Server when installed on same host (Linux)?

## [Case 1](/docs/mdicap/v5.14.1/knowledge-base/how-to-set-up-ignition-file-for-both-md-core-and-md-icap-server-#case-1)

Requirement:

- MD Core and MD ICAP Server are installed on same host
- MD Core and MD ICAP Server will use separate PostgreSQL database

Solution:

- Database of MD Core

  - Database type: local
  - Database port: (default) **5432**
  - Database username: postgres
  - Database password: your_own_pg_password_of_core
- Database of MD ICAP Server

  - Database type: local
  - Database port: (default) **5433 - must be difference from MD Core**
  - Database username: postgres
  - Database password: your_own_ICAP_pg_password

| Product | Ignition content |
| --- | --- |
| MD Core  path: /etc/opswat/ometascan.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**local**  host=**localhost**  port=**5432**  user=**postgres**  password=**your_own_pg_password_of_core** |
| MD ICAP Server  path: /etc/opswat/mdicapsrv.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**local**  host=**localhost**  port=**5433**  user=**postgres**  password=**your_own_ICAP_pg_password** |

## [Case 2](/docs/mdicap/v5.14.1/knowledge-base/how-to-set-up-ignition-file-for-both-md-core-and-md-icap-server-#case-2)

Requirement:

- MD Core and MD ICAP Server are installed on same host
- MD Core uses local PostgreSQL database
- MD ICAP Server will connect to MD Core's PostgreSQL database

Solution:

- Database of MD Core

  - Database type: local
  - Database port: (default) **5432**
  - Database username: postgres
  - Database password: your_own_pg_password_of_core
- Database of MD ICAP Server

  - Database type: remote
  - Database port: (default) **5432 - must be same as MD Core**
  - Database username/password: same as MD Core

| Product | Ignition content |
| --- | --- |
| MD Core  path: /etc/opswat/ometascan.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**local**  host=**localhost**  port=**5432**  user=**postgres**  password=**your_own_pg_password_of_core** |
| MD ICAP Server  path: /etc/opswat/mdicapsrv.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**remote**  host=**localhost**  port=**5432**  user=**postgres**  password=**your_own_pg_password_of_core** |

## [Case 3](/docs/mdicap/v5.14.1/knowledge-base/how-to-set-up-ignition-file-for-both-md-core-and-md-icap-server-#case-3)

Requirement:

- MD Core and MD ICAP Server are installed on same host
- MD Core and MD ICAP Server will connect to remote PostgreSQL database

Solution:

- Database of MD Core

  - Database type: **remote**
  - Database port: Port of remote PostgreSQL (e.g: **5432**)
  - Database username/password: username/password of remote PostgreSQL server
- Database of MD ICAP Server

  - Database type: **remote**
  - Database port: Port of remote PostgreSQL (e.g: **5432**)
  - Database username/password: username/password of remote PostgreSQL server

E.g:

- Remote PostgreSQL :

  - Host: **192.168.1.10**
  - Port: **5432**
  - Username: **postgres**
  - Password: **your_own_remote_pg_password**

| Product | Ignition content |
| --- | --- |
| MD Core  path: /etc/opswat/ometascan.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**remote**  host=**192.168.1.10**  port=**5432**  user=**postgres**  password=**your_own_remote_pg_password** |
| MD ICAP Server  path: /etc/opswat/mdicapsrv.conf | eula=true  [global]  dbmode=1  [user]  name=admin  password=admin  email=admin@local  [dbserver]  type=**remote**  host=**192.168.1.10**  port=**5432**  user=**postgres**  password=**your_own_remote_pg_password** |
