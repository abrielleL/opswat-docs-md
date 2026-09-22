<!-- source: https://www.opswat.com/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a -->

# Why is my licensed users in EGS increasing automatically , not able to process emails

Check your version
This article applies to MetaDefender Email Gateway Security (EGS) deployments where inbound email processing relies on a licensed user count.

## [**Symptoms**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#symptoms)

EGS stops processing emails, and affected messages are held and repeatedly retried instead of being delivered.

The EGS log shows email retry entries classified as `NO_LICENSE`, similar to the following:

[SOC ] 2026.05.29 08:11:53.472: (email.retry) Email retry, classifications='NO_LICENSE', email_id='206810', message_id='N/A', next_retry='2026-05-29 06:12:23 UTC', processing_id='1533d357cqcf4279b2R02688ba4ecc4f', recipients='recipient@recipientaddress.com', retry_count='2', sender='sender@senderaddress.com', subject='Email Subject' [msgid: 0]

The `NO_LICENSE` classification indicates that EGS has no available license slot for the user associated with the message, so it cannot process the email.

## [**Root cause**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#root-cause)

The licensed user limit has been reached. When every license slot is consumed, EGS has no free slot to assign to a valid user, and the affected emails are classified as `NO_LICENSE` and queued for retry instead of being processed.

A common contributing factor is the **Auto-Assign Licensed Users** feature. When enabled, EGS automatically detects email recipients and adds them to the licensed user list. Over time this can fill the available slots with invalid or unintended users, leaving no capacity for the users who actually need to be licensed.

## [**Resolution**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#resolution)

Free up license capacity and prevent it from being consumed automatically.

### [**1. Review and clean up the licensed user list**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#1-review-and-clean-up-the-licensed-user-list)

Verify the current licensed user count against your entitlement, then remove invalid or unintended users so that EGS has enough free slots for all valid users.

### [**2. Disable Auto-Assign Licensed Users**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#2-disable-auto-assign-licensed-users)

Disable the **Auto-Assign Licensed Users** function under **Settings → MetaDefender Email Gateway Security**. This stops EGS from automatically detecting email recipients and adding them to the licensed user list, which prevents license slots from being consumed by invalid or unintended users.

Pasted image 20260620190447.png

After freeing up slots and disabling auto-assignment, EGS should be able to assign licenses to valid users, and the retried emails will be processed on their next retry cycle.

## [**Please note**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#please-note)

- Re-enabling Auto-Assign Licensed Users will cause the licensed user list to grow automatically again. Leave it disabled if you want to manage licensed users manually.
- If all slots are legitimately in use, the licensed user count itself may be undersized for your environment. Review your licensing entitlement before removing users you still need.

## [**Support**](/docs/mdemail/knowledge-base/why-is-my-licensed-users-in-egs-increasing-automatically---not-a#support)

If you need further assistance, please contact OPSWAT Support through the [OPSWAT Portal](https://my.opswat.com/) or your assigned support representative.
