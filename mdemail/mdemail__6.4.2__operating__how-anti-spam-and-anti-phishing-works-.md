<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works- -->

# How anti-spam and anti-phishing works?

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Overview](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#overview)

Over 90% of all cyberattacks start with an email.

In the reconnaissance phase, cybercriminals try to harvest information from the organization. Very often they use phishing emails to obtain credentials to gain a foothold within the organization.

[<https://www.lockheedmartin.com/en-us/capabilities/cyber/cyber-kill-chain.html>]

### [What is spam and phishing?](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#what-is-spam-and-phishing)

**Spamming** is the use of messaging systems to send an unsolicited message (spam) to large numbers of recipients for the purpose of commercial advertising, for the purpose of non-commercial proselytizing, or for any prohibited purpose (especially the fraudulent purpose of phishing). [<https://en.wikipedia.org/wiki/Spamming>]

Most email spam messages are commercial in nature. Whether commercial or not, many are not only annoying, but also dangerous because they may contain links that lead to phishing web sites or sites that are hosting malware - or include malware as file attachments. [<https://en.wikipedia.org/wiki/Email_spam>]

Email spam has steadily grown since the early 1990s, and by 2014 was estimated to account for around 90% of total email traffic. Since the expense of the spam is borne mostly by the recipient, it is effectively postage due advertising. [<https://en.wikipedia.org/wiki/Email_spam>]

**Phishing** is the fraudulent attempt to obtain sensitive information or data, such as usernames, passwords and credit card details, by disguising oneself as a trustworthy entity in an electronic communication. Typically carried out by email spoofing, instant messaging, and text messaging, phishing often directs users to enter personal information at a fake website which matches the look and feel of the legitimate site.

Phishing is an example of social engineering techniques used to deceive users. Users are lured by communications purporting to be from trusted parties such as social web sites, auction sites, banks, colleagues, executives, online payment processors or IT administrators. [<https://en.wikipedia.org/wiki/Phishing>]

Phishing –being potentially harmful unsolicited messages– can be seen as a subset of spamming.

### [Multi-layer anti-spam and anti-phishing approach](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#multi-layer-anti-spam-and-anti-phishing-approach)

Applying multiple layers in protection is a widely adopted approach in information security in general. As phishing is one of the most severe threat vectors today, Email Gateway Security applies the same approach against it.

If a spam or phishing email can get through the previous layer, then the next, even more stringent layer is there to counter it.

## [Phishing & spam filtering](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#phishing--spam-filtering)

The filtering layer gets rid of emails that are known to be spam or phishing and as so have no business value. Beyond the fact that these emails may be harmful and have no value at all from the business perspective, their removal significantly reduces the load on the subsequent layers' processing components.

### [Overview](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#overview)

#### [Approach](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#approach)

Spam waves usually last for a very limited time. Sometimes a spam site lives for a few hours only before it gets detected and shut down. Under this short lifespan, a spam wave can cause significant harm to the victims, and even an update every fifteen minutes may not be fast enough to catch most of them. This is the reason why it has the utmost importance to keep spam filters continuously up-to-date.

An on-premises solution is simply unable to keep the update pace. Frequent updates require processing capacity (CPU, RAM) and load the internal network with the distribution. That is the reason why MetaDefender Email Gateway Security uses a cloud-based approach.

Our servers performing the detection are updated very frequently: up to every five minutes; and there is no load at all on-premises.

No language dependency

Given by the nature of the spam filters, the spam detection technologies used by MetaDefender Email gateway security are not language dependent.

#### [Update workflow](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#update-workflow)

1. Spammers start a new campaign updating their **botnet** with new spam templates.
2. The army of zombie machines starts sending spam.
3. Our system gathers millions of unsolicited emails daily through

   1. Spam traps,
   2. Honeypots and
   3. External spam feeds.
4. Every spam is processed and sent to automated training systems.
5. The filters are updated.

Filters with proactive detection

Filters based on machine learning algorithms have proactive detection and do not need updates for every new spam campaign.

#### [Performance](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#performance)

Beyond the very high update performance (up to every five minutes, as mentioned below), our spam filter has one of the best spam accuracy. Our spam catch rate is over 99.9% while the false positive rate is 0.00%.

| **Performance indicator / success factor** | **Value** |
| --- | --- |
| Update frequency | ~5 minutes |
| Replication time | 3-5 seconds |
| Spam catch rate | 99.9% |
| False positive rate | 0.00% |
| Language dependency | None |

#### [Privacy](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#privacy)

Emails may contain sensitive data. The spam filtering technology used by MetaDefender Email Gateway Security was developed following a privacy-by-design approach.

Our spam filtering technology extracts hashes and anonymized pieces of information from the email. This is then used as input to statistic calculations and heuristics. Only the received headers and the URLs in the email body are used in their original form for detection reasons.

**Information sent to the cloud**

To successfully detect spam, some information is necessary to be transmitted to the cloud for the detection. No content of the original e-mail body and no information which could be used to identify a specific person is transmitted. The following information is transmitted to the cloud for each scanned e-mail message:

- The IP address of the sender of the original e-mail (obtained from the e-mail headers);
- The e-mail message fingerprint which is a set of cryptographical hashes on different parts of the e-mail headers and body. The hashes are irreversible, and no original email body is transmitted;
- URLs contained in the body of the scanned e-mail message;
- MD5 hashes of e-mail addresses and telephone numbers contained in the body of the scanned e-mail message;
- MD5 hashes of the *From* address, *From* domain and *Reply-To* address (obtained from the e-mail headers);
- Hashes of the images embedded into the e-mail, if any. This is required to detect the image-based spam such as when the spam message is inside the attached picture. The images are not transmitted;
- MD5 hashes of certain types of attachments (e.g. office documents, pdf documents, executables), if any. This is required to detect e-mails containing the spam message inside these types of attachments;
- File names of attachments when a potentially harmfully file is detected (e.g. Windows executables).

### [Text fingerprint filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#text-fingerprint-filter)

The text fingerprint filters are based on the text that is present in the email’s From and Subject headers and in the email body. The filter creates an extract from these parts of the email, and creates a hash fingerprint.

The hashing algorithm is designed to generate very similar fingerprints for similar pieces of text. This way we can counter the spam technique when spammers apply slight modifications to the text to circumvent anti-spam technologies. If a new fingerprint is similar to a previously known spam fingerprint, then the new fingerprint belongs to spam as well with a good chance.

Poison detection

Our text fingerprint filters apply a poison detection mechanism to ignore irrelevant text.

Visual normalization

Our text fingerprint filters apply character visual normalization to counter the common spam technique when spammers try to change words in their written form - making them hard to detect by computers - while the meaning of the word will still be the same with a good chance.

**Example**

Original word: OPSWAT

Spam version: 0PSWAT (note the zero instead of the capital O in the head of the word).

### [IP reputation filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#ip-reputation-filter)

IP reputation checking is a traditional method to counter spam. Known spam senders are listed on blocklists (i.e. DNS Real-time Blackhole Lists (DNSRBLs), Domain Name System Blocklists (DNSBLs), Real-time Blackhole Lists (RBLs) etc.), and if the sending IP of the email is on the blocklist, then the email is categorized as spam.

The IP reputation system used by Email Gateway Security is based on own and external spam and threat intelligence feeds and reports from the wild. Additional techniques, as reverse DNS lookups and passive DNS can also help to associate IPs and domains and to build detection patterns.

The IP detection is not directly related to the type of the spam campaign, IPs of spammers are on the blocklist irrelevant of the kind of their activity.

Proactive detection

Our systems are able to identify characteristics of a spam wave and proactively add detection for IPs that will probably soon be used in sending spam emails.

### [URL and domain reputation filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#url-and-domain-reputation-filter)

This filter checks the reputation of the URLs in the email body and the reputation of the domains of these URLs. Similarly to IP reputation, URL reputation data comes from own and external spam and threat intelligence feeds and reports from the wild.

#### [Domain detection](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#domain-detection)

Based on HTML page structure, traffic, lifespan, reputation of the IPs used, whois information, registrant email address, TLD reputation, etc. for any domain can it can be decided if it is a spammer domain or not.

Emails with any URLs of a spammer domain are considered spam.

#### [URL detection](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#url-detection)

URL detection is the filter for cases where we do not treat the whole domain as spammer. It is for cases for example, when legit domains are exploited, hacked, infected a controlled detection is needed. In this case exact URLs are blocklisted for example for

- *Shortening*,
- *Free hosting* and
- *File sharing* domains

#### [Domain reputation](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#domain-reputation)

#### [URL reputation](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#url-reputation)

As the following diagrams summarize, the main difference between domain and URL reputation is that while:

- in case of domain reputation the whole domain with all subdomains and URLs is treated as spammer,
- in case of URL reputation each URL is handled separately, the domain itself may or may not be treated as spammer.

### [Attachment filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#attachment-filter)

The attachment spam filter is something similar to what traditional anti malware does. In addition to traditional anti-malware, attachment filter is also prepared to specific phishing cases, as it can detect HTML bank forms for example. The attachment filter can unpack archives and inspect archived files.

### [Email address filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#email-address-filter)

Initially created for Nigerian and lottery scams, now very useful in detecting other kind of spam, e.g. : fake sales, spear phishing, dating, employment, loan, etc.

The email addresses are extracted from the body of the message and from the *Reply-To* and *From* headers of the email (it is a common phishing technique to redirect replies using the Reply-To header).

Using machine learning, heuristics and clustering methods waves using spammer addresses are identified and the proper email addresses are blocklisted.

Most exploited

The most exploited free webmail domains are gmail.com, yahoo.com, yandex.ru, qq.com and hotmail.com.

### [Image filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#image-filter)

It is a common technique to send the whole spam email as a single image. This way it is much harder for anti-spam technologies to find out the contents and to classify an email as a spam.

Also, in spam and phishing messages there are recurring image contents that when can be detected, it is easier to classify an email as spam or phishing.

Blocklisting methods are based on image characteristics, for example size, resolution, color distribution, compression, etc.

Our technologies include:

- Optical character recognition (OCR): this technology can extract text from images. Useful in detecting stock, extortion, pharmacy, advertising spam, etc.
- Similar image detection: based on color histogram, similar, but not identical images can be detected and classified as spam or phishing For example it is a common spam technique to make the spam image blurry or add color pixels to it (while it is still readable) to make its detection difficult.

[<https://www.nirsoft.net/articles/spam/viagra_spam.html>]

[<https://www.nirsoft.net/articles/spam/viagra_spam.html>]

- Face detection and recognition: combined with other, specific email characteristics this technology can help to classify attached images and detect spam campaigns like *Russian brides* scams
- Logo recognition: this technique can prevent image false-positives, and can be used to identify phishing scams. For example it is a common technique to send phishing emails on behalf of a well known service provider, like eFax.

[<https://threatpost.com/microsoft-office-365-credentials-attack-fax/162232/>]

### [Phone number filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#phone-number-filter)

In nature similar to IP and domain blocklists, this is a blocklist of phone numbers used mostly in Russian and Asian spam. These numbers are usually extremely obfuscated and need special regular expressions to be extracted from emails.

There is also a database of prefixes and telecom operators for targeted countries.

### [Cryptocurrency filter](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#cryptocurrency-filter)

Cryptocurrency wallet addresses are frequently used in scam emails. The victims are usually instructed to make the payments to these wallet addresses. Cryptocurrency wallets are typical in extortion spam, a very aggressive, new type that evolved from sextortion to even bomb threats.

## [Content disarm & reconstruction](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#content-disarm--reconstruction)

Content Disarm & Reconstruction (CDR) , also known as data sanitization, is a computer security technology that removes potentially malicious code from files. CDR assumes all files are malicious and sanitizes and rebuilds each file ensuring full usability with safe content. Unlike malware analysis, CDR technology does not determine or detect malware's functionality but removes all file components that are not approved within the system's definitions and policies and that has the potential to contain malicious code (e.g. macros in Microsoft Office documents, JavaScript in PDF documents, **hyperlink references in HTML**, etc.).

OPSWAT Deep CDR technology is a market leader with superior features like multi-level archive processing, accuracy of file regeneration, and support for 100+ file types. OPSWAT provides in-depth views of what is being sanitized and how, enabling choices and define configurations that meet the use-case. Safe files are delivered with 100% of threats eliminated within milliseconds, so the workflow is not interrupted.

For further details see <https://en.wikipedia.org/wiki/Content_Disarm_%26_Reconstruction> and <https://www.opswat.com/technologies/data-sanitization>.

Email Gateway Security provides

- *hyperlink reference listing* or
- *hyperlink reference removal, and*
- *attachment disarm and reconstruction*

as counter-phishing techniques for the 0.1% of spam that successfully slipped through our spam filters.

### [Hyperlink reference listing](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#hyperlink-reference-listing)

Using Deep CDR, this technique gathers all the hyperlink references (visible and invisible ones - e.g. those that are hidden behind an image) within the email body, and displays them together in one place.

The benefit is that the user can review the real hyperlink references, can spot the potentially malicious ones, and can make an informed decision about the risk level of clicking any of them.

The drawback of this technique is that the links are still clickable - accidentally or deliberately - within the email body.

#### [Before (Sent)](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#before-sent)

#### [After (Received)](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#after-received)

Note the list of hyperlinks from the email body collected together at the bottom of the email.

The original hyperlinks are still fully functional.

### [Hyperlink reference removal](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#hyperlink-reference-removal)

Using Deep CDR, this technique removes all the hyperlink references (visible and invisible ones - e.g. those that are hidden behind an image) within the email body, and adds the hyperlink reference as text.

The benefit is that the user can review the real hyperlink references, can spot the potentially malicious ones, and can make an informed decision about the risk level of visiting the referenced pages. It is also a benefit, that the links can not be clicked.

The drawback of this technique is that the links are not clickable, if the user wants to visit a referenced page, the reference must be copied to a browser.

Risk of working links

Some email clients can be configured to interpret URLs as hyperlinks, where there is no hyperlink reference, or even for text-only emails. In case of such a configuration it can turn out, that links defused by Email Gateway security are rendered by the client in a way that the resulted links are functional, exposing email recipients to the risk of falling victim to phishing attacks.

**Example**

Microsoft Outlook auto-formats URLs to hyperlinks by default. To disable this feature go to **File / Options / Mail / Editor Options / Proofing / AutoCorrect Options / AutoFormat** and disable the option *Internet and network paths with hyperlinks* (see the image below).

#### [Before (Sent)](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#before-sent)

#### [After (Received)](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#after-received)

Note the hyperlink references added as plain text between brackets in the email body text. Even the link hidden under the image can be displayed and disarmed with this technique.

The original hyperlinks are defused, clicking them results in no event.

### [Attachment disarm & reconstruction](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#attachment-disarm--reconstruction)

Some phishing attacks use attached documents as weaponized content instead of hyperlinks.

Email Gateway Security splits an email to separate files of:

- the header,
- the body (for each of the text and HTML rendition in case of HTML formatted emails), and
- the attachments.

These files are then sent to Deep CDR for processing. Deep CDR assumes all the headers, body and attachments are malicious and sanitizes and rebuilds each file ensuring full usability with safe content. When the email recipient opens the attached document, is is safe already.

## [URL reputation checks](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#url-reputation-checks)

Using MetaDefender Cloud's URL reputation services Email Gateway Security can block phishing emails at the time these emails are processed or when the recipient clicks on links in the email.

### [On-arrival URL analysis](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#on-arrival-url-analysis)

The results of the on-arrival URL reputation checks are merged with the results of the phishing filtering.

When the URL reputation services find malicious URLs in an email, then the email is classified as *Phishing* and the Phishing/Spam verdict will list Malicious URL among the verdicts.

The *Processing history* section of the *Email details* gives some insights about the URL reputation check outcome (e.g. which providers found threats).

The on-arrival URL reputation check works independent from the phishing filtering (i.e. it can work even when there is an anti-phishing engine failure).

### [Time-of-click analysis](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#time-of-click-analysis)

If a malicious link reaches the recipient despite of all the countermeasures above, and the recipient clicks or opens it, MetaDefender Cloud’s Safe URL Redirect service is still there as a final line of defense.

This solution can also be effective against the threats that were yet unknown at the time of spam-filtering and Deep CDR processing.

For details see the *MetaDefender Cloud Safe URL redirect* section under [Operating/Phishing and spam](/docs/mdemail/6.4.2/operating/phishing-and-spam).

## [Display name spoofing detection](/docs/mdemail/6.4.2/operating/how-anti-spam-and-anti-phishing-works-#display-name-spoofing-detection)

Using MetaDefender Core's YARA engine, Email Gateway Security can detect display name spoofing attacks.

For each protected sender a YARA rule needs to be created that can detect the anomalies of the display name and the sender email address. These YARA rules need to be imported into Core.

When an email is detected with the display name spoofed, Email Gateway Security will give a YARA classification.

The *Show results* link can give more details which sender caused the hit.
