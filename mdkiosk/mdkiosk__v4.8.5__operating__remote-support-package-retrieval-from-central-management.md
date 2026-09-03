<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/remote-support-package-retrieval-from-central-management -->

# Remote Support Package Retrieval from Central Management

# [Remote Support Package Retrieval from Central Management](/docs/mdkiosk/v4.8.5/operating/remote-support-package-retrieval-from-central-management#remote-support-package-retrieval-from-central-management)

If your Kiosk device is enrolled in Central Management (CM10) and running Kiosk 4.8.1 or later, you can generate and download a support package remotely — without needing direct network access to the Kiosk itself. This is useful when the Kiosk is on a restricted network, or when you're supporting many devices at once.

## [Prerequisites](/docs/mdkiosk/v4.8.5/operating/remote-support-package-retrieval-from-central-management#prerequisites)

- The Kiosk device must be enrolled in Central Management.
- MetaDefender Kiosk 4.8.1 or later must be installed on the device.
- The Kiosk device must be active and connected to Central Management at the time you request the package.

## [Retrieving a Support Package](/docs/mdkiosk/v4.8.5/operating/remote-support-package-retrieval-from-central-management#retrieving-a-support-package)

1. Sign in to Central Management.
2. From your account menu, open **Help Center**.
3. Select the **Support Package** tab.
4. Click **Create Support Package**.
5. Choose **Kiosk Windows** and select the device (or devices) you want a package from, using their Deployment ID.
6. Wait for generation to complete — progress is shown while the package is being created.
7. Once it's ready, download the package directly from Central Management, or delete it if you no longer need it.

Note

Support packages generated this way are stored on Central Management, separately from any packages downloaded locally on the Kiosk. Each account can keep up to 10 packages; once that limit is reached, the oldest one is automatically removed to make room for a new request.

## [Retrieving a Support Package Locally](/docs/mdkiosk/v4.8.5/operating/remote-support-package-retrieval-from-central-management#retrieving-a-support-package-locally)

You can also generate and download a support package directly from an individual Kiosk's own console, without Central Management enrollment — see [How do I create a support package for MetaDefender Kiosk?](https://www.opswat.com/docs/mdkiosk/knowledge-base/how-do-i-create-a-support-package-for-metadefender-kiosk-)
