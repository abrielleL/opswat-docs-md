<!-- source: https://www.opswat.com/docs/mdemail/6.4.1/operating/frequently-asked-questions -->

# Frequently asked questions

## [What is sanitization (content disarm & reconstruction)?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#what-is-sanitization-content-disarm--reconstruction)

Sanitization, or content disarm and reconstruction (CDR) is a detection-less, zero-trust technique that removes potentially malicious contents from email bodies and attached files.

Emails often contain seemingly harmless hyperlinks and document attachments that can easily used to exploit human error in phishing attacks. CDR is one of the most efficient technologies to remove potentially malicious components form email bodies and file attachments.

For details see [Deep CDR](https://docs.opswat.com/mdcore/deep-cdr).

## [What can I do when my email was blocked?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#what-can-i-do-when-my-email-was-blocked)

Your email was blocked cause it violated your organization's policy in a way that requires blocking. For example: your email contains malware or sensitive data.

Your blocked email is withheld by Email Gateway Security in a special, malware resistant storage called Quarantine.

If you need your email then you may have the following options:

1. Turn to your administrators and ask releasing your email, or
2. In your *Email blocked* notification email click on the quarantine actions link and then on the *Quarantine actions* page select either the *Release quarantined email* or the *Request release of quarantined email* action (if you have any of them available), or

3. In your *Quarantine report* click on the Actions link and on the the *Quarantine actions* page select either the *Release quarantined email* or the *Request release of quarantined email* action (if you have any of them available).

For details see [Email recipient guide](/docs/mdemail/6.4.1/operating/recipient-guide).

## [How to get encrypted attachments delivered?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#how-to-get-encrypted-attachments-delivered)

Attackers often encrypt attachments to hide malicious contents. An encrypted attachment is a random sequence of bits, anti-malware scanners, sandboxes and other security technologies are unable to deal with them. Encrypted attachments need to be decrypted first so that they can be processed.

If your email contains encrypted attachments, then the email gets blocked, and you are notified about the blocked email in a notification. The notification contains a link, where you can provide the password to your encrypted attachments to decrypt them.

Once the attachments are successfully decrypted, a rescan is automatically initiated on them. If an attachment —after the rescan— turns out to be clean (no malware, no sensitive data, etc.) then it gets automatically delivered to you.

For details see [Email recipient guide](/docs/mdemail/6.4.1/operating/recipient-guide).

## [Why are attachments missing from my email?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#why-are-attachments-missing-from-my-email)

Email attachments are popular means of delivering malware or phishing to or leaking sensitive data from organizations.

At certain organizations Email Gateway Security is set up in a way, that in case of problems with attachments (infected, password protected, contain sensitive data, etc.) not the whole email gets blocked, only the problematic attachments get removed.

Disclaimers will always inform you when problematic attachments have been removed from your email. For details about disclaimers see [Email recipient guide](/docs/mdemail/6.4.1/operating/recipient-guide).

In some cases attachments get replaced in the email with image placeholders or tombstone files. For these cases see [Tombstone files](/docs/mdemail/6.4.1/configuration/policy#advanced-threat-prevention) section for details.

## [What are the black bars covering some info in my email?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#what-are-the-black-bars-covering-some-info-in-my-email)

Emails and attachments may contain sensitive data and your organization's policy may be to block these pieces of sensitive data.

In such a case, Email Gateway Security will hide the sensitive data inside email bodies and attachments behind black bars (we call it redaction) but otherwise deliver the email.

For details see [Email recipient guide](/docs/mdemail/6.4.1/operating/recipient-guide).

## [How to get my original file when it was sanitized?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#how-to-get-my-original-file-when-it-was-sanitized)

Email Gateway Security withholds the original copy of sanitized emails.

If you need the original copy —with the potentially malicious contents— you can turn to your administrators asking for releasing the original copy of your sanitized email.

## [How can I even so visit my sanitized hyperlinks?](/docs/mdemail/6.4.1/operating/frequently-asked-questions#how-can-i-even-so-visit-my-sanitized-hyperlinks)

Sanitized hyperlinks are always in the format of

`<original anchor label> (<hyperlink reference>)`, for example

`google.com (https://metadefender.opswat.com/safe-redirect/www.opsvvat.com)`.

If you really want to visit the sanitized hyperlink:](If you really want to visit the sanitized hyperlink:

1. Verify the URL within the brackets (verify only what is behind [https://metadefender.opswat.com/safe-redirect/](%60https://metadefender.opswat.com/safe-redirect/%60))
2. If the URL looks valid, then copy the whole URL within the brackets and paste it into a browser's address bar.
