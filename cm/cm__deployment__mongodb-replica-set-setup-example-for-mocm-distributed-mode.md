<!-- source: https://www.opswat.com/docs/cm/deployment/mongodb-replica-set-setup-example-for-mocm-distributed-mode -->

# MongoDB Replica Set Setup Example for MOCM Distributed Mode

> **Info**
>
> This is an example setup for deploying a MongoDB 8.x Replica Set for MOCM Distributed Mode. Adapt the values (IPs, ports, paths, credentials) to match your environment. For detailed MongoDB installation, refer to the official documentation links below

## 1. Prerequisites

### 1.1 Environment Requirements

| **Component** | **Requirement** |
| ---- | ---- |
| MongoDB Version | 8.0.x (Community or Enterprise) |
| Number of Nodes | 3 (minimum for production) |
| Supported OS | RHEL 8/9, Rocky Linux 8/9, Ubuntu 22.04/24.04, Windows Server 2019/2022 |
| RAM | Minimum 16 GB per node (32 GB recommended) |
| Disk | Minimum 100 GB free space (SSD recommended) |
| Network | All nodes must communicate on TCP port 27017 |

### 1.2 Hostname Planning

| **Role** | **IP (example)** |
| ---- | ---- |
| Primary | 10.40.160.159 |
| Secondary | 10.40.160.160 |
| Secondary | 10.40.160.161 |

> **MongoDB 5.0+ IP Address Note**
>
> Starting from MongoDB 5.0, nodes configured with only IP addresses fail startup validation by default. To use IP addresses without DNS hostnames, you must add the following startup parameter in `mongod.conf` / `mongod.cfg`:
>
> setParameter:
>
> disableSplitHorizonIPCheck: true
>
> This parameter is included in the configuration in Section 5.

## 2. Install MongoDB 8.x

> **Perform on ALL 3 nodes**
>
> Follow the official MongoDB installation guide for your operating system.

| **Operating System** | **Official Installation Guide** |
| ---- | ---- |
| RHEL / Rocky Linux | [https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-red-hat/) |
| Ubuntu | [https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-ubuntu/) |
| Windows | [https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/](https://www.mongodb.com/docs/manual/tutorial/install-mongodb-on-windows/) |

After installation, **do not start** the MongoDB service yet. Proceed to configure TLS and keyfile first.

## 3. Generate TLS Certificate

> **Info**
>
> Perform on one machine, then distribute to all nodes. If your organization already has a PKI/CA infrastructure, use your existing CA to sign the MongoDB server certificates. Skip to Step 3.2.

### 3.1 Create Certificate Authority (CA]

```javascript
mkdir -p /etc/mongodb/ssl && cd /etc/mongodb/ssl

# Generate CA key and certificate (valid 10 years)
openssl genrsa -out ca.key 4096
openssl req -new -x509 -days 3650 -key ca.key -out ca.crt \
  -subj "/C=US/ST=California/L=SanFrancisco/O=YourOrganization/OU=IT/CN=MongoDB-CA"
```

### 3.2 Generate Server Certificate (per node]

Repeat for each node (mongo1, mongo2, mongo3), replacing values:

```javascript
# Example for node 10.40.160.159
openssl genrsa -out mongo1.key 4096

openssl req -new -key mongo1.key -out mongo1.csr \
  -subj "/C=US/ST=California/L=SanFrancisco/O=YourOrganization/OU=MongoDB/CN=10.40.160.159"

# SAN extension (REQUIRED - must include IP)
cat > mongo1-ext.cnf <<EOF
[v3_req]
subjectAltName = @alt_names
[alt_names]
IP.1 = 10.40.160.159
EOF

# Sign with CA
openssl x509 -req -in mongo1.csr -CA ca.crt -CAkey ca.key \
  -CAcreateserial -out mongo1.crt -days 3650 \
  -extensions v3_req -extfile mongo1-ext.cnf

# Create PEM (key + cert combined - required by MongoDB)
cat mongo1.key mongo1.crt > mongo1.pem
```

> **Repeat for other nodes**
>
> Replace `mongo1` with `mongo2`/`mongo3` and update the IP value:
>
> - mongo2: `10.40.160.160`
> - mongo3: `10.40.160.161`

### 3.3 Distribute Certificates

| **File** | **Copy to** |
| ---- | ---- |
| ca.crt | All 3 nodes |
| mongo1.pem | mongo1 only |
| mongo2.pem | mongo2 only |
| mongo3.pem | mongo3 only |

**Certificate directory:**

- Linux: `/etc/mongodb/ssl/`
- Windows: `C:\MongoDB\ssl\`

**Set permissions (Linux):**

```javascript
sudo chown -R mongod:mongod /etc/mongodb/ssl/
sudo chmod 600 /etc/mongodb/ssl/*.pem /etc/mongodb/ssl/*.key
sudo chmod 644 /etc/mongodb/ssl/ca.crt
```

## 4. Generate Keyfile for Internal Authentication

```javascript
# Generate (on one node)
openssl rand -base64 756 > mongodb-keyfile
```

Copy the **same keyfile** to all 3 nodes:

- Linux: `/etc/mongodb/ssl/mongodb-keyfile` (chmod 400, owned by mongod)
- Windows: `C:\MongoDB\ssl\mongodb-keyfile`

```javascript
# Linux - set permissions
sudo chmod 400 /etc/mongodb/ssl/mongodb-keyfile
sudo chown mongod:mongod /etc/mongodb/ssl/mongodb-keyfile
```

## 5. Configure MongoDB (mongod.conf / mongod.cfg)

This is the **critical configuration** specific to MOCM deployment. Apply on **all 3 nodes**.

### 5.1 Linux Configuration

```javascript
# /etc/mongod.conf
storage:
  dbPath: /var/lib/mongo

systemLog:
  destination: file
  logAppend: true
  path: /var/log/mongodb/mongod.log

net:
  port: 27017
  bindIp: 0.0.0.0
  tls:
    mode: requireTLS
    certificateKeyFile: /etc/mongodb/ssl/mongo1.pem
    CAFile: /etc/mongodb/ssl/ca.crt
    allowConnectionsWithoutCertificates: true

security:
  keyFile: /etc/mongodb/ssl/mongodb-keyfile
  authorization: enabled

replication:
  replSetName: "rs0"

setParameter:
  disableSplitHorizonIPCheck: true

processManagement:
  timeZoneInfo: /usr/share/zoneinfo
```

### 5.2 Windows Configuration

```javascript
# C:\Program Files\MongoDB\Server\8.0\bin\mongod.cfg
storage:
  dbPath: C:\MongoDB\data

systemLog:
  destination: file
  logAppend: true
  path: C:\MongoDB\log\mongod.log

net:
  port: 27017
  bindIp: 0.0.0.0
  tls:
    mode: requireTLS
    certificateKeyFile: C:\MongoDB\ssl\mongo1.pem
    CAFile: C:\MongoDB\ssl\ca.crt
    allowConnectionsWithoutCertificates: true

security:
  keyFile: C:\MongoDB\ssl\mongodb-keyfile
  authorization: enabled

replication:
  replSetName: "rs0"

setParameter:
  disableSplitHorizonIPCheck: true
```

### 5.3 Key Configuration Parameters

| **Parameter** | **Value** | **Description** |
| ---- | ---- | ---- |
| net.tls.mode | requireTLS | All connections must use TLS |
| net.tls.allowConnectionsWithoutCertificates | true | Clients don't need client cert (set false for mutual TLS) |
| security.keyFile | path to keyfile | Internal authentication between replica set members |
| security.authorization | enabled | Enforce role-based access control |
| replication.replSetName | rs0 | Must be identical on all nodes |
| setParameter.disableSplitHorizonIPCheck | true | Required when using IP addresses instead of hostnames |
| net.bindIp | 0.0.0.0 | Listen on all interfaces |

## 6. Start MongoDB and Initialize Replica Set

### 6.1 Start Service on All Nodes

```javascript
# Linux
sudo systemctl enable mongod
sudo systemctl start mongod
sudo systemctl status mongod

# Windows
# If service config was updated, reinstall service first:
& "C:\Program Files\MongoDB\Server\8.0\bin\mongod.exe" --remove
& "C:\Program Files\MongoDB\Server\8.0\bin\mongod.exe" --config "C:\Program Files\MongoDB\Server\8.0\bin\mongod.cfg" --install --serviceName "MongoDB"

Start-Service MongoDB
```

### 6.2 Initialize Replica Set

Connect to **10.40.160.159** using `mongosh` with TLS:

```javascript
mongosh --host 10.40.160.159 --port 27017 \
  --tls --tlsCAFile /etc/mongodb/ssl/ca.crt \
  --tlsCertificateKeyFile /etc/mongodb/ssl/mongo1.pem
```

Run:

```javascript
rs.initiate({
  _id: "rs0",
  members: [
    { _id: 0, host: "10.40.160.159:27017" },
    { _id: 1, host: "10.40.160.160:27017" },
    { _id: 2, host: "10.40.160.161:27017" }
  ]
})
```

### 6.3 Verify

```javascript
rs.status()
```

**Expected: 1 PRIMARY + 2 SECONDARY**

## 7. Create Users for MOCM

> **Warning**
>
> Create users immediately after rs.initiate(). The localhost exception closes after the first user is created.

Connect to the **PRIMARY** node and run:

```javascript
// Create Admin User
use admin
db.createUser({
  user: "adminUser",
  pwd: "CHANGE_ME_STRONG_PASSWORD",
  roles: [
    { role: "userAdminAnyDatabase", db: "admin" },
    { role: "clusterAdmin", db: "admin" },
    { role: "readWriteAnyDatabase", db: "admin" }
  ]
})
```

## 8. Connection String for MOCM

GUI "Database Address" Field

```javascript
10.40.160.159:27017,10.40.160.160:27017,10.40.160.161:27017
```

## 9. Configure MOCM Installer - Database Configuration

After MongoDB Replica Set is ready, enter the following values in the *"My OPSWAT Central Management Setup"* installer:

| Field | Value |
| ---- | ---- |
| Database Address | 10.40.160.159:27017,10.40.160.160:27017,10.40.160.161:27017 |
| Connection Type | *Discovery* |
| Database Admin Username | The admin user created in Step 7 |
| Password | The admin password created in Step 7 |

## 9. Verification & Troubleshooting

### 9.1 Test Connection

```javascript
mongosh "mongodb://metadefender:PASSWORD@10.40.160.159:27017,10.40.160.160:27017,10.40.160.161:27017/admin?replicaSet=rs0&authSource=admin" \
  --tls --tlsCAFile /etc/mongodb/ssl/ca.crt
```

### 9.2 Common Issues

| **Issue** | **Solution** |
| ---- | ---- |
| Service fails to start | Check logs: `/var/log/mongodb/mongod.log` or `C:\MongoDB\log\mongod.log` |
| Keyfile permission error (Linux) | `chmod 400` and `chown mongod:mongod` |
| TLS handshake failure | Verify SAN in cert matches hostname in rs.initiate() |
| Members can't connect | Check firewall, verify hostname resolution between nodes |
| "not authorized" | Ensure you created users before localhost exception closed |

### 9.3 Useful Command

```javascript
rs.status()        // Replica set health
rs.conf()          // Current replica set config
db.serverStatus()  // Server metrics
```
