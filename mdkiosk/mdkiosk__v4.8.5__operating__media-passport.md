<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/operating/media-passport -->

# Media Passport

MetaDefender Kiosk can generate a **Media Passport** — a one-page summary attached to a scan session's report — so that someone checking a device at a security checkpoint can see whether it's cleared without reading a full scan report. The verdict, expiration, and key session details are all on a single page, with the allowed/rejected result shown clearly at the top. Available starting in Kiosk 4.8.2.

## [Enabling the Media Passport](/docs/mdkiosk/v4.8.5/operating/media-passport#enabling-the-media-passport)

1. In the Kiosk Web Management Console, go to **Configuration > Report**.
2. Expand the **Session Log** section.
3. Under **Include Media Passport**, select **Enable Media Passport**.
4. Enter a **Media Passport validity period**, in days.
5. Optionally, select **Reject media if there are hidden or unmounted partitions** and/or **Include QR code**.
6. Click **Save Updates**.

Once enabled, the Media Passport is added automatically as the first page of the session report for standard scan sessions — no separate action is needed at the Kiosk itself.

## [Media Passport Options](/docs/mdkiosk/v4.8.5/operating/media-passport#media-passport-options)

| Setting | Description | Default |
| --- | --- | --- |
| Enable Media Passport | Turns the feature on. When off, session reports are generated exactly as before, with no passport page. | Disabled |
| Media Passport validity period | How many days a passport remains valid after it's issued, from 1 to 3650 days. Kiosk prints the resulting expiration date on the passport so a reviewer can tell if an older passport has expired. | — |
| Reject media if there are hidden or unmounted partitions | When on, a device with a hidden or unmounted partition is treated as failing the passport check, even if every partition Kiosk could scan came back clean. | Disabled |
| Include QR code | Adds a QR code to the passport. Requires entering the text to encode (up to 500 characters) in the field that appears; you can include the same variables available elsewhere in Session Log settings, such as the current user's name. | Disabled |

Note

The **Reject media if there are hidden or unmounted partitions** setting only applies to full scans of the media; behavior for other scan types isn't affected by this option. When the setting is off (the default), a hidden or unmounted partition is still shown to the user as an on-screen notice during the session — it just doesn't by itself cause the Media Passport to be rejected.

## [Issuing an Exempted Passport](/docs/mdkiosk/v4.8.5/operating/media-passport#issuing-an-exempted-passport)

Sometimes a device needs to be let through a checkpoint even though it hasn't been scanned — for example, when an approved exception is already in place. MetaDefender Kiosk supports this with two settings that work together: hiding a workflow from the normal selection screen, and letting an operator skip scanning entirely and receive a passport marked **Exempted**.

### [Hiding a workflow](/docs/mdkiosk/v4.8.5/operating/media-passport#hiding-a-workflow)

An administrator can set up a workflow that isn't shown on the Kiosk's regular workflow list, but is still available to the specific people assigned to it.

1. In the Kiosk Web Management Console, go to **Workflows**.
2. In the **Employee Workflow** or **Guest Workflow** section, turn on **Use additional options**. A **Hide** column appears next to each workflow in that list.
3. Select **Hide** on the workflow you want to keep off the regular selection screen.
4. Click **Save**.

A hidden workflow still works exactly like any other workflow once selected — it's just not shown by default. At least one workflow must always stay visible in each category, and the **Default** workflow can never be hidden.

On the Kiosk itself, anyone assigned to a hidden workflow sees a **Hidden Workflow** icon on the menu bar. Tapping it opens the hidden workflow(s) for selection without needing to sign in again. You can change where this icon appears (or turn it off) under **Configuration > Kiosk UI**, in the menu bar customization list.

### [Letting a session skip scanning](/docs/mdkiosk/v4.8.5/operating/media-passport#letting-a-session-skip-scanning)

An administrator can also allow a specific workflow to be completed without inserting media or scanning at all.

1. On the Workflows page, open the workflow you want to update.
2. Go to the **Media Types** tab.
3. Turn on **Skip Processing**.
4. Click **Save**.

This setting works the same way whether or not the workflow is also hidden — they're independent options you can use together or separately.

When **Skip Processing** is turned on, a **Skip Processing** button appears on the screens leading up to media insertion. Selecting it opens a short email confirmation step, and then completes the session immediately — no device needs to be inserted or scanned. The resulting Media Passport shows an **Exempted** result instead of Allowed or Rejected, along with the date it was issued, the person who completed the session, and up to four of that workflow's user-question answers if any are configured. Since no media was involved, the device details on an Exempted passport (model name, media type, and disk usage) show as not applicable.

Note

A full Media Passport PDF and its record in your session history are only produced when your Session Log is set to PDF format and **Include Media Passport** is turned on. Without that, skipping processing still completes the session and sends a confirmation email, but no passport file is attached.

## [What's on the Media Passport](/docs/mdkiosk/v4.8.5/operating/media-passport#whats-on-the-media-passport)

The passport is designed to be understood in a few seconds. It includes:

- An **Allowed/Rejected** result, shown with a color and an icon at the top of the page.
- The **expiration date**, based on the scan date and the validity period you configured.
- The **Kiosk** that performed the scan and the **session ID**.
- **User information** — user ID, display name, and email address, where available.
- **Media information** — the device's model name, media type (for example, USB or SD card), and disk usage/partition details.
- **Scan details** — scan type, workflow used, the date and time of the scan, and the number of files processed, allowed, and blocked.

Note

For sessions signed in through a Guest or Custom authentication workflow, the user ID field on the passport may appear blank depending on how that workflow is configured.

## [Example](/docs/mdkiosk/v4.8.5/operating/media-passport#example)

A security desk wants every USB drive brought into a restricted area to carry proof it was scanned that day. The administrator enables the Media Passport with a 1-day validity period. After each scan, the resulting passport shows that day's scan date and a same-day expiration — so a passport from a previous visit is clearly no longer valid, and staff can tell at a glance whether a new scan is required before the device is allowed in.

Note

The Media Passport is added to scans performed through standard scanning workflows. It is not generated for Self-Scan sessions or for sessions that only retrieve files without scanning media.
