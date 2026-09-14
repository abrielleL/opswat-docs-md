<!-- source: https://www.opswat.com/docs/mdss/4.4.2/configuration/notifications -->

# Notifications

In order to send email notifications, make sure that an SMTP server is available. Please see [SMTP](/docs/mdss/4.4.2/configuration/smtp) for more details.

To enable notifications follow these steps:

1. Navigate to **Settings -> Notifications**
2. Choose the event for which you wish to receive notifications. There are two types of notifications, each having different possible configurations:

   1. Email notifications, which can be sent:

      1. When a report is generated. Please see [Email reports](/docs/mdss/4.4.2/configuration/email-reports).
      2. When a user registration request is pending an administrator approval
      3. When a file is blocked while processing a storage. Please see [Blocked file notifications](/docs/mdss/4.4.2/configuration/blocked-file-notifications).
   2. Webhook notifications, which can be sent:

      1. When a scan is completed. Please see [Scan completed Notifications](/docs/mdss/4.4.2/configuration/scan-completed-notifications)
      2. When a file is completed. Please see [File scanned Notifications](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/configuration/file-scanned-notifications)
   3. RabbitMQ notification which can be sent when a file is completed. Please see [File scanned RabbitMQ Notifications](/docs/mdss/4.4.2/metadefender-storage-security/4.3.0/configuration/file-scanned-rabbitmq-notifications)
