<!-- source: https://www.opswat.com/docs/md-ot-security/v.2.2.6/settings/alert -->

# Alert

## [Alert](/docs/md-ot-security/v.2.2.6/settings/alert#alert)

Alert setting is accessible under **Settings > Alert.**

On alert setting page, user can configure how MetaDefender OT Security behave when there is an alert triggered: make on screen alert, notify operator by sending email and send syslog message.

## [**Make on-screen alert**](/docs/md-ot-security/v.2.2.6/settings/alert#make-on-screen-alert)

You can choose how alerts can be displayed:

- On-screen alert is enabled: you will be navigated to the alert screen whenever there is an alert triggered, regardless of role user are, on any other screens, and all the alerts need to be resolved to be able to leave the alert screen.
- On-screen alert is disabled: alerts will only appear in alert list pages with an Acknowledge button beside so that user can resolve them later.

In addition, you can customize:

- At what criticality levels, there will be on-screen alert.
- At what criticality levels, a reason need to be provided when acknowledge an alert.

Note: Alert with low criticality will not be shown on screen by default.

## [**Send syslog message**](/docs/md-ot-security/v.2.2.6/settings/alert#send-syslog-message)

Enable Send syslog message on if you want MetaDefender OT Security to send you syslog message.

Fill in the server address and port to receive the syslog.

You can also choose for Facility of syslog message.

## [**Send email alert**](/docs/md-ot-security/v.2.2.6/settings/alert#send-email-alert)

Enable Send email if you want MetaDefender OT Security to send you alert email for alerts in the system.

Fill in the SMTP server address and port to receive the email.

Fill in the SMTP credentials if have.

You can see the email template by click on Button Preview email.

## [**Email Scheduling**](/docs/md-ot-security/v.2.2.6/settings/alert#email-scheduling)

Here user can set:

- The time to receive notification emails since there is an alert in the system (e.g. set for 15 seconds if you want to receive a notification email after 15 seconds since the alert happened)
- Each email will notify for one or many alerts by using sending mode individual/batch.
