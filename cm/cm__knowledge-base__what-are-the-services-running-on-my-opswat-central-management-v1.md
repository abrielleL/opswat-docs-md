<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-are-the-services-running-on-my-opswat-central-management-v1 -->

# What are the services running on My OPSWAT Central Management v10 in RedHat/Rhel?

> **Check Your Version:**
>
> This article applies to all My OPSWAT Central Management releases deployed on RedHat/Rhel systems.

## **Overview**

My OPSWAT Central Management includes many systemd units. For health checks, most services are expected to be **active**; the essential services below summarize the key units to verify. The only expected different state is `mocm-systemd-monitor.service`, which may appear as **activating** with **auto-restart**.

| UNIT | LOAD | ACTIVE | SUB | DESCRIPTION |
| ---- | ---- | ---- | ---- | ---- |
| Most MOCM services | loaded | active | running | Expected state for the majority of MOCM services. |
| mocm-nginx.service | loaded | active | running | Web server / reverse proxy. |
| mocm-tomcat.service | loaded | active | running | Core application service. |
| mocm-mongodb.service | loaded | active | running | Database service. |
| mocm-rabbitmq.service | loaded | active | running | Messaging service. |
| mocm-valkey.service | loaded | active | running | Cache service. |
| mocm-systemd-monitor.service | loaded | activating | auto-restart | Expected different state; this service can be seen restarting automatically. |
| mocm-all.target / mocm-infra.target | loaded | active | active | Target units for all MOCM and infrastructure services. |
| mocm-otelcol-gate.timer | loaded | active | waiting | Telemetry reconciliation timer. |

 

## **Troubleshooting**

If services remain in an inactive, activating or stopped state, please restart the services by running the command

```powershell
sudo systemctl restart mocm-all.target
```

 

If issues persist, please generate a support package and contact support as shown below.

Support package: [How to generate a support package for My OPSWAT Central Management? - My OPSWAT Central Management](https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme)

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
