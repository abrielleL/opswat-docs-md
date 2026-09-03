<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/why-is-my-md-kiosk-disabled-on-secure-image-and-how-to-resolve-i -->

# Why is my MD Kiosk disabled on Secure Image and how to resolve it?

This article applies to all MD Kiosk Secure Image versions

One of the unique features of the Secure Image is File Integrity Monitoring, which is integrated with the Kiosk UI. The system continuously monitors the Kiosk installation folder for unauthorized modifications. If any unauthorized action is detected, it will be blocked, a signal will be sent to the Kiosk service, and the Kiosk UI will be terminated immediately. The following error message will be displayed:

**How to resolve this situation**:

When this screen appears, the administrator must close the Kiosk UI to access the Kiosk console locally or connect to it remotely from another computer.

From the Console, find Settings > Logs > File Integrity Event. Then you will see the list of detected actions that caused the Kiosk disabled.

After verifying that the reason for the modification has been investigated, you can select **Acknowledge Event** to confirm and clear the existing alerts. You may then start the Kiosk launcher

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
