<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/why-is-the-discovery-service-becoming-unresponsive-due-to-rabbit -->

# Why is the Discovery Service becoming unresponsive due to RabbitMQ connection issues?

> **Check Your Version:**
>
> This article applies to MetaDefender Secure Storage version older than 4.1.0 deployed on Windows and Linux systems.

## Issue:

The Discovery Service becomes unresponsive or stops working. Log entries show timeout and retry messages in the PublishHandler, along with RabbitMQ connection errors such as:

```plaintext
Already closed: The AMQP operation was interrupted
Close reason: code=406
```

## Possible Causes:

- Missing or misconfigured target exchange in RabbitMQ.
- Transient network interruptions or broker restarts leading to dropped connections.
- RabbitMQ reaching connection or channel limits, causing timeouts.

## Resolution:

Upgrade the Helm chart to use MDSS version 4.1.0. This version includes fixes for Discovery Service stability and RabbitMQ connection handling.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
