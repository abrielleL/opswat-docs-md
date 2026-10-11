<!-- source: https://www.opswat.com/docs/mdss/knowledge-base/how-to-set-up-active-active-configuration- -->

# How to set up Active Active configuration?

> **Check Your Version:**
>
> This article applies to all MetaDefender Storage Security version deployed in both Linux or Windows.

**Summary:** Guide for Configuring MDSS Active-Active Setup

**Description:** Below is a detailed guide to configure an Active-Active setup for MDSS, along with a recommended startup approach to ensure stability.

---

### **Step 1 — Deploy External Services**

Set up the following services on dedicated servers (separate from MDSS nodes):

- **PostgreSQL** — Install and create the MDSS database and user
- **RabbitMQ** — Install and create a user with appropriate permissions
- **Redis** — Install and configure a password for remote access

Reference documentation: [External Services Configuration - MetaDefender Storage Security](https://www.opswat.com/docs/mdss/installation/external-services-configuration)

---

### **Step 2 — Configure MDSS to Use External Services**

On each MDSS node, update the `/etc/mdss/customer.env` file:

```plaintext
# External RabbitMQ
RABBITMQ_URI=amqp://<user>:<password>@<rabbitmq_host>:5672
RABBITMQ_HOST=<rabbitmq_host>
RABBITMQ_PORT=5672
RABBITMQ_DEFAULT_USER=<user>
RABBITMQ_DEFAULT_PASS=<password>

# External Redis
CACHE_SERVICE_URI=<redis_host>:6379,user=default,password=<password>,syncTimeout=10000
CACHE_SERVICE_URL=<redis_host>
CACHE_SERVICE_PORT=6379

# External PostgreSQL
POSTGRES_HOST=<postgres_host>
POSTGRES_PORT=5432
POSTGRES_DB=mdss
POSTGRES_USER=<user>
POSTGRES_PASSWORD=<password>
```

---

### **Step 3 — Disable Bundled Services**

Since external services are used, disable the built-in services:

`DISABLED_SERVICES=postgres,rabbitmq,redis`

This ensures each MDSS node does not start local instances.

---

### **Step 4 — Start MDSS Nodes (Recommended Approach)**

To ensure stable initialization:

1. Start only **one MDSS node** first
2. Verify all services are running properly
3. Perform a test scan (e.g., upload a sample file)
4. Once validated, start additional nodes using the same configuration

---

### **Step 5 — (Optional) Load Balancer**

A load balancer is optional but recommended:

- Provides high availability for Web UI/API via a single endpoint
- Should include health checks (e.g., port 443)

**Note:** Not required for scanning, as workload distribution is handled via RabbitMQ.

---

### **Step 6 — (Optional) Automate Active-Passive Failover**

If your requirement is failover rather than parallel processing, a reference script is available that monitors the active node and triggers a scan on the passive node once the active one stops responding:

[OPSWAT/mdss-active-passive-failover](https://github.com/OPSWAT/mdss-active-passive-failover)

Configuration is done entirely through `PASSIVE_MODE_*` environment variables (required: active and passive URLs and ports, API key, storage ID, workflow ID and scan name; optional: priority, check interval, request timeout and failure threshold). The repository README documents the prerequisites, every variable and how to run the script as a service.

---

### **How It Works**

- File events (e.g., RTP) are published to the shared RabbitMQ queue
- The first available MDSS node processes the request
- All nodes share the same PostgreSQL database, ensuring consistent state and no duplicate scanning

> **Support:**
>
> If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer.**](https://my.opswat.com/portal/support-services)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
