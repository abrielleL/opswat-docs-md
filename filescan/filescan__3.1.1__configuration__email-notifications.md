<!-- source: https://www.opswat.com/docs/filescan/3.1.1/configuration/email-notifications -->

# Email Notifications

It is possible to get email notifications about completed scan reports. This can also be done selectively for reports with specific verdicts.

Please use your SMTP server credentials when configuring the following properties in `/home/sandbox/sandbox/broker.cfg`:

BashCopy#############################
# Email Notification settings
#
# Note: use '--test-email' CLI to test the smtp settings
#############################
smtpServer=
smtpPort=465
smtpUser=
smtpPass=
smtpUseSSL=true
smtpUseStartTLS=false
smtpDebugEnabled=true
# Note: specify a list of emails separated by comma (e.g. "analyst1@domain.com,analyst2@domain.com")
notifyEmails=
notifyEmailsIgnoreDomains=
# Note: use 'ALL' to notify on any verdict
notifyEmailsOnVerdicts=LIKELY_MALICIOUS,MALICIOUS
# Note: if enabled, whenever a report is generated for a msg/eml/rfc822 file, the "to" address is notified in addition to 'notifyEmails'
notifyEmailSenderOfEmailFiles=false
notifyEmailReceiverOfEmailFiles=false
notifyEmailsDefaultSender=noreply@mydomain.com
# Note: if enabled, whenever a report is generated for a msg/eml/rfc822 file, the "from" header will be set to the original sender
notifyEmailsUseOriginalSender=false
# Note: the following placeholder may be used: $SHA-256
# e.g. notifyEmailsIncludeUrlInAlert=https://www.filescan.io/search-result?query=$SHA-256
notifyEmailsIncludeUrlInAlert=

This is an excerpt from an example email notification about a likely malicious scan report:

BashCopyFrom: <noreply@filescan.io>
Subject: [FSIO] Completed analysis for 'pafish.exe' (Task ID: 5f709158-c08f-4fb9-a43f-597873aedef2): { "verdict": "LIKELY_MALICIOUS", "threatLevel": 0.75, "confidence": 1 }
---------------------------- Analysis Overview ----------------------------
fsBroker version: 1.1.0-2f62d72
SHA-256: 9e7d694ed87ae95f9c25af5f3a5cea76188cd7c1c91ce49c92e25585f232d98e
Submit ID: d6809fa3-e226-4484-b07b-1f68ba259a46
Task ID: 5f709158-c08f-4fb9-a43f-597873aedef2
Date: 2023-10-291 07:52+0000291
submitName: pafish.exe
mediaType:
{
"string": "application/x-msdownload; format\u003dpe32",
"slash": 11,
"semicolon": 24,
"parameters": {
"format": "pe32"
}
}
---------------------------- Report Overview ----------------------------
overallState:
"SUCCESS"
finalVerdict:
{
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
allTags:
[
{
"source": "YARA_RULE",
"sourceIdentifier": "9e7d694ed87ae95f9c25af5f3a5cea76188cd7c1c91ce49c92e25585f232d98e",
"isRootTag": false,
"tag": {
"name": "anti-vm",
"synonyms": [],
"descriptions": [],
"verdict": {
"verdict": "UNKNOWN",
"threatLevel": 0,
"confidence": 1
}
}
},
{
"source": "OSINT_LOOKUP",
"sourceIdentifier": "9e7d694ed87ae95f9c25af5f3a5cea76188cd7c1c91ce49c92e25585f232d98e",
"tag": {
"name": "hlux",
"synonyms": [],
"descriptions": [],
"verdict": {
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
},
{
"source": "OSINT_LOOKUP",
"sourceIdentifier": "9e7d694ed87ae95f9c25af5f3a5cea76188cd7c1c91ce49c92e25585f232d98e",
"tag": {
"name": "khalesi",
"synonyms": [
"KPOT Stealer",
"kpot"
],
"verdict": {
"verdict": "LIKELY_MALICIOUS",
"threatLevel": 0.75,
"confidence": 1
}
}
}
]

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
