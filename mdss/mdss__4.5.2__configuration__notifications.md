<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/notifications -->

# Notifications

> **Info**
>
> In order to send email notifications, make sure that an SMTP server is available. Please see [SMTP](https://www.opswat.com/docs/mdss/configuration/smtp) for more details.

To enable notifications follow these steps:

1. Navigate to **Settings -> Notifications**
2. Choose the event for which you wish to receive notifications. There are two types of notifications, each having different possible configurations:
   1. Email notifications, which can be sent:
      1. When a report is generated. Please see [Email reports](https://www.opswat.com/docs/mdss/configuration/email-reports).
      2. When a user registration request is pending an administrator approval
      3. When a file is blocked while processing a storage. Please see [Blocked file notifications](https://www.opswat.com/docs/mdss/configuration/blocked-file-notifications).
   2. Webhook notifications, which can be sent:
      1. When a scan is completed. Please see [Scan completed Notifications](https://www.opswat.com/docs/mdss/configuration/scan-completed-notifications)
      2. When a file is completed. Please see [File scanned Notifications](https://www.opswat.com/docs/mdss/configuration/file-scanned-notifications)
   3. RabbitMQ notification which can be sent when a file is completed. Please see [File scanned RabbitMQ Notifications](https://www.opswat.com/docs/mdss/configuration/file-scanned-rabbitmq-notifications)

![](https://uploads.developerhub.io/prod/k8zL/267oiaj9u6g7fxvxjhaz2s4s7lfw63afhzid7jqxuicce5dm7cyq05m3amj4ip1s.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
