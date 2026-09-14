<!-- source: https://www.opswat.com/docs/mdemail/integrations/onsite-microsoft-exchange-deployment -->

# Onsite Microsoft Exchange deployment

## [Overview](/docs/mdemail/integrations/onsite-microsoft-exchange-deployment#overview)

Limitations

MetaDefender Email Gateway Security can only be installed on Hub or Edge role Exchange Servers (2013 or 2016).

For prerequisites and installation instructions see [Installation/Prerequisites](/docs/mdemail/installation/prerequisites).

Exchange autodetect

Email Gateway Security autodetects when it is installed on a machine where Exchange server is present. In this case it will install in Exchange mode, no manual setup is needed.

## [Exchange Server message expiration timeout](/docs/mdemail/integrations/onsite-microsoft-exchange-deployment#exchange-server-message-expiration-timeout)

The *MessageExpirationTimeout* parameter of Microsoft Exchange Server specifies the maximum time that a particular message can remain in a queue.

MessageExpirationTimeout

If a message remains in the queue for longer than the *MessageExpirationTimeout* period of time, the message is returned to the sender as a permanent failure.

As a consequence this parameter is likely to affect the delivery of emails released or forwarded from **Quarantine** (see [Operating/Quarantine](/docs/mdemail/operating/quarantine)) or emails retried from **Audit > Email History** (see [Operating/Email History](/docs/mdemail/operating/email-history)).

The default value of *MessageExpirationTimeout* is 2 days. It means that if an email spends more than 2 days in **Quarantine** or in **Audit > Email History** then releasing or forwarding and retrying (accordingly) after 2 days will fail.

Extension

*MessageExpirationTimeout* can be extended to the maximum of 90 days.

Low values

If *MessageExpirationTimeout* is set to a very low value (the lowest accepted value is 5 seconds) then it can even affect the delivery of emails going through the normal workflow (not quarantined, not failing).

## [Reference and further reading](/docs/mdemail/integrations/onsite-microsoft-exchange-deployment#reference-and-further-reading)

Microsoft Exchange Server 2013: <https://technet.microsoft.com/en-us/library/bb124238(v=exchg.150).aspx>

Microsoft Exchange Server 2016: <https://technet.microsoft.com/en-us/library/bb124238(v=exchg.160).aspx>

## [How To Verify](/docs/mdemail/integrations/onsite-microsoft-exchange-deployment#how-to-verify)

To verify that the Exchange Transport Agent has been installed successfully, open the Exchange Management Shell and enter Get-TransportAgent

Ensure that *MetaDefender Email Security Smtp Agent* and *MetaDefender Email Security Routing Agent* are listed and their *Enabled* statuses are *True*.

[PS] C:\Windows\system32>Get-TransportAgent
Identity Enabled Priority
-------- ------- --------
Transport Rule Agent True 1
DLP Policy Agent True 2
Malware Agent False 3
Text Messaging Routing Agent True 4
Text Messaging Delivery Agent True 5
System Probe Drop Smtp Agent True 6
System Probe Drop Routing Agent True 7
Metadefender Email Security Smtp Agent True 8
Metadefender Email Security Routing Agent True 9
