<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/when-is-the----database-maintenance-required----notification-tri -->

# When Is the “Database Maintenance Required” Notification Triggered, and How Does the ometascan-vacuum-db Tool Improve Performance?

This article applies to **MetaDefender Core version 5.12.0** and above

Administrators can configure Email Notification settings to receive alerts about detected threats and incidents, providing real-time updates on potential security risks.

The **Database Monitor** keeps users informed about the current database status and notifies them when a vacuum process is required to maintain optimal performance.

For additional information about configuring email notifications, refer to:

[**→ Email Notification**](https://www.opswat.com/docs/mdcore/configuration/email-notification)

## [When Is the “Database Maintenance Required” Notification Triggered?](/docs/mdcore/knowledge-base/when-is-the----database-maintenance-required----notification-tri#when-is-the-database-maintenance-required-notification-triggered)

This notification is sent when the database accumulates a significant amount of obsolete data that could degrade performance or increase disk usage. Specifically, the trigger is based on a fixed threshold of **200,000 dead tuples**.

**Dead tuple monitoring process**:

- The system checks for dead tuples every hour.
- If the number of dead tuples exceeds the threshold, a “Database Maintenance Required” email notification is sent.
- After the notification is sent, the next check will occur after 24 hours.

**Example:** Each time a file scan result is deleted from the Scan History, the number of dead tuples increases. When these deleted entries reach 200,000 and the scheduled check interval has passed, the system automatically triggers a notification.

---

## [What Happens When Running the ometascan-vacuum-db Tool, and How Does It Improve Performance?](/docs/mdcore/knowledge-base/when-is-the----database-maintenance-required----notification-tri#what-happens-when-running-the-ometascan-vacuum-db-tool-and-how-does-it-improve-performance)

Running the `ometascan-vacuum-db` tool removes obsolete row versions (dead tuples), reclaims unused storage space, and updates table statistics. This helps the database query planner operate more efficiently and ensures smoother performance.

**Key benefits include:**

- Reduced database size on disk
- Faster query execution for reporting, UI access, and scan record retrieval
- Improved overall responsiveness of MetaDefender Core

---

## [Conclusion](/docs/mdcore/knowledge-base/when-is-the----database-maintenance-required----notification-tri#conclusion)

Regular database maintenance is essential to ensuring consistent system performance and reliability. The “**Database Maintenance Required**” notification provides an early warning that helps prevent potential slowdowns caused by data fragmentation. By running the `ometascan-vacuum-db` tool promptly after receiving the notification, administrators can optimize storage usage, maintain faster query speeds, and enhance the overall efficiency of **MetaDefender Core**.

Keeping your database clean and well-maintained not only improves responsiveness but also contributes to a more stable and scalable environment.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
