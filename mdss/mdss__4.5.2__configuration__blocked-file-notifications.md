<!-- source: https://www.opswat.com/docs/mdss/4.5.2/configuration/blocked-file-notifications -->

# Blocked file notifications

Blocked files notifications are sent for each blocked file that is found during an Instant, Scheduled or Real-Time processing.

To enable notifications for blocked file, select the option to **Blocked Files** from the **Email Notifications** section:

![](https://uploads.developerhub.io/prod/k8zL/e3pycpnita7qgnnk3tei0zay7gwoutk6xbc3d4ub6p176pfwlcg7hwo9uvvir5hr.png)

You can choose to send this email to:

- All MetaDefender Storage Security registered users
- Only to the file owner
- To the file owner and all MetaDefender Storage Security registered users

> **Info**
>
> Please note that the notification to the file owner could be sent only for OneDrive, Box and MFT integrations.

The email contains the following information:

- File name
- File path
- Storage unit type and name
- The reason why the file is blocked
- [Remediation](https://www.opswat.com/docs/mdss/configuration/workflows)  actions details (delete/move blocked files), when these are configured for the storage that is processed

![](https://image-archive.developerhub.io/image/upload/v2_5262/m48drbe0pnuea0yba2rg/1633421404.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
