<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder- -->

# How to reduce the size of /data/queuestore folder?

This article applies to all MetaDefender Email Gateway Security V4 and V5 releases deployed on Windows Systems.

The `/data/queuestore` folder directory stores emails that are either quarantined or pending delivery in Email Gateway Security. Over time, this folder can grow significantly, especially if there are many quarantined or failed emails. This article explains why the storage grows and provides steps to reduce its size safely.

## [Why the Queue Storage Grows](/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder-#why-the-queue-storage-grows)

- **Quarantined Emails:** Emails held for review or flagged by security policies remain in the folder until cleared.
- **Pending Delivery Emails:** Emails awaiting delivered are temporarily stored here.
- **Failed Emails:** Repeated delivery failures can cause the email to permanently fail and remain stored.

***Note:*** The files in this folder are required for normal Email Gateway Security operation. Deleting them manually may disrupt email delivery.

## [How to Reduce Queue Storage Size](/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder-#how-to-reduce-queue-storage-size)

#### [**1.** **Manual Cleanup of Email History**](/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder-#1-manual-cleanup-of-email-history)

You can perform a manual cleanup of email history to remove older or failed emails:

- Go to **Audit > Email History > Cleanup**

- Select a **retention date span**

- Click **Start**

***Note:*** Depending on the size of your email history, this process may take several hours to complete.

#### [**2. Configure Shorter Retention**](/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder-#2-configure-shorter-retention)

Reducing the retention period for quarantined emails can prevent the folder from growing too large:

- Navigate to **Settings > Data Retention > locate Failed emails cleanup schedule, Quarantine cleanup schedule**
- Set a shorter retention span (e.g., 1 week instead of the default 4 weeks)

**You can also clean up quarantine emails manually:**

1. Go to **Quarantine > Cleanup**
2. Choose the desired **retention time**

Regularly managing email history and quarantine retention ensures `/data/queuestore` folder remains at a manageable size, improves system performance, and prevents unnecessary storage growth

## [**Verify the Change:**](/docs/mdemail/knowledge-base/how-to-reduce-the-size-of--data-queuestore-folder-#verify-the-change)

- Navigate to `/data/queuestorefolder`.
- Right-click the folder and select **Properties**.

- Note the current file size before applying any changes.

- After applying the changes, check the folder again, you will see that the file size has decreased.

Support:

If Further Assistance is required, please proceed to [**create a support case or chat with our support engineer**](https://my.opswat.com/support).
