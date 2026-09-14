<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-reset-the-kiosk-app-exit-password-if-i-forget-it- -->

# How do I reset the Kiosk App exit password if I forget it?

This article is applied to Kiosk App and Kiosk Hardened Image releases deployed on Windows systems.

**Issue:** Forgetting the Kiosk App's exit password.

**Resolution:** There are a couple of methods to reset the exit password.

- **Over the network:** Try accessing the Web Management Console directly from a remote machine by navigating to `http(s)://<kiosk_IP_or_hostname>:8009/` in a web browser. You can then disable the exit password.
- **Reboot in Safe Mode**

  - Power on the computer.
  - *Interrupt boot 3 times:*

    - As soon as the Windows logo appears, **force-shutdown** by holding the power button for **5–10 seconds**.
    - Repeat this **twice more** (3 total interrupted boots).
  - On the 4th boot, Windows enters **Automatic Repair**.
  - Navigate to: `Troubleshoot → Advanced options → Startup Settings → Restart`.
  - After restart, press:

    - `F4` for *Safe Mode*.
    - `F5` for *Safe Mode with Networking*.

Note:

Booting into Safe Mode is only possible if you are **not** using the Kiosk Hardened Image.

- **Re-Image:** If you **are** using the Kiosk Hardened Image and the network method doesn’t work, you will need to re-image the Kiosk from scratch.

  - Please refer to this document step-by-step guidance: <https://www.opswat.com/docs/mdkiosk/hardened-image/guideline---deploying-kiosk-hardened-image>.

Caveat:

Re-imaging the kiosk will delete all your previous settings.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/portal/support).
