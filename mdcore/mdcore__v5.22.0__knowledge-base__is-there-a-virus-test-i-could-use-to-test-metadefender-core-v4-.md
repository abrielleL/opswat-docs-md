<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/is-there-a-virus-test-i-could-use-to-test-metadefender-core-v4- -->

# Is there a virus test I could use to test MetaDefender Core engines?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows or Linux systems.

Please Note:

Tests to determine an engine's operation should not be run with live malware. The suggested approach is to test using an industry standard test file called an **EICAR Test File**, which most antivirus engines detect as positive - even though no threat exists.

An **EICAR Test File** can be downloaded from [here](https://www.eicar.org/download-anti-malware-testfile/). You can also create your own version of the file by copying the following string into a file and renaming the file ‘**eicar.com**’.

X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*Pro Tip:

For more information about the EICAR Test File, please visit the European Expert Group for IT-Security's [Website](http://2016.eicar.org/86-0-Intended-use.html)**.**

**Please take note that the EICAR file could be blocked by the localAV, so for testing purposes you should exclude it as a threat.**

Support:

If you’re having any trouble testing MetaDefender Core’s included **Scan Engines**, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
