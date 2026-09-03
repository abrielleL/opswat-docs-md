<!-- source: https://www.opswat.com/docs/mdicap/knowledge-base/why-do-only-some-files-from-my-nutanix-file-share-not-show-up-in -->

# Why do only some files from my Nutanix file share not show up in the ICAP or MetaDefender Core Scan History?

#### [**Why can’t I access my Nutanix file after Core has scanned it?**](/docs/mdicap/knowledge-base/why-do-only-some-files-from-my-nutanix-file-share-not-show-up-in#why-cant-i-access-my-nutanix-file-after-core-has-scanned-it)

**Background**

Nutanix sends each file to ICAP, either

- Every time the file is uploaded and/or downloaded
- Until the file is explicitly marked "Blocked" by ICAP, or
- *Until Nutanix gets a reply from ICAP that it doesn’t know how to process. This is any value outside of “No Threat Detected”, or “Blocked”.*

*In the 2nd and 3rd cases above, the file will be immediately Quarantined by Nutanix as well, and never automatically rescanned. They will remain in this state permanently, or until manually unquarantined via the Nutanix Console.*

#### [**Use case one**](/docs/mdicap/knowledge-base/why-do-only-some-files-from-my-nutanix-file-share-not-show-up-in#use-case-one)

The file is sent to ICAP which gets a correct Blocked verdict from Core.

**Expected behavior**

File is permanently Quarantined on the Nutanix side and never submitted for a rescan. File becomes locked until unlocked by an admin.

#### [Use case two](/docs/mdicap/knowledge-base/why-do-only-some-files-from-my-nutanix-file-share-not-show-up-in#use-case-two)

The file is sent to ICAP, which either can’t respond for reasons of its own, or receives a different response from Core other than “No Threat Detected”, or “Blocked”.

For example, a 503 error or explicit Failed to Scan result from Core.

**Expected behavior**

Nutanix marks the file with an Unknown response, which also triggers the Quarantine behavior described above.

Once again Nutanix locks the file permanently until reset by an administrator and does not submit the file for rescan.

#### [What can we do about it?](/docs/mdicap/knowledge-base/why-do-only-some-files-from-my-nutanix-file-share-not-show-up-in#what-can-we-do-about-it)

**Nutanix side**

Nutanix Support can provide tools to help unquarantine and scan all previously quarantined files.

**OPSWAT side**

Open a Support Case.

Include screenshots of the scan results on MD Core from the first time the file is scanned.

Collect a Support Package from MD Core and MD ICAP server (see **Support** below). Your agent will provide an upload link.

We can help determine where the unexpected response comes from.

*If there is no first scan, Core might have been down or unavailable when the scan was first attempted.*

If Core was up at the time, one classic scenario is that the file Failed to Scan when it was first submitted. This can be caused by a number of factors, many of which are outlined in the KB article below.

[**Why do my files show Failed to Scan in Metadefender Core?**](https://opswat.atlassian.net/wiki/spaces/DDK/pages/4056416569/Why+are+files+from+my+Nutanix+file+share+not+showing+in+ICAP+MetaDefender+Core+Scan+History+and+why+are+they+inaccessible+after+scanning)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).

How to create a Support Package for MD Core: [MetaDefender Core Support Package](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-)

How to create a Support Package for MD ICAP Server: [MetaDefender ICAP Server Support Package](https://www.opswat.com/docs/mdicap/troubleshooting/how-to-create-support-package)
