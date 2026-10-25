<!-- source: https://www.opswat.com/docs/mdemail/6.4.2/operating/phishing-and-spam -->

# Phishing and spam

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Anti-phishing](/docs/mdemail/6.4.2/operating/phishing-and-spam#anti-phishing)

### [Classifications](/docs/mdemail/6.4.2/operating/phishing-and-spam#classifications)

The following classifications are applied to (potential) phishing emails:

- Phishing
- Possible phishing
- Anti-phishing failure
- SPF Fail
- SPF Soft fail
- SPF Error
- SPF No record
- SPF Neutral
- SPF Pass
- DKIM Invalid
- DKIM Error
- DKIM No signature
- DKIM Valid

For details see [Operating/Email classifications](/docs/mdemail/6.4.2/operating/email-classifications).

### [Handling of phishing emails](/docs/mdemail/6.4.2/operating/phishing-and-spam#handling-of-phishing-emails)

Based on the configuration, Email Gateway Security can handle (potential) phishing emails in the following ways:

- Reject,
- Delete,
- Quarantine or
- Deliver.

For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

### [Phishing subcategories](/docs/mdemail/6.4.2/operating/phishing-and-spam#phishing-subcategories)

For certain phishing email, Email Gateway Security is able to tell the phishing subcategory of the email.

#### [Supported subcategories](/docs/mdemail/6.4.2/operating/phishing-and-spam#supported-subcategories)

| Subcategory | Description |
| --- | --- |
| Spear Phishing | E-mail messages categorized as spear phishing includes targeted phishing emails like: spear phishing, business email compromise, sender impersonation, CEO/CFO executive whaling. |
| Extortion | E-mail messages categorized as extortion includes sextortion, blackmail, hitman scams etc. |
| Financial Phishing | E-mail messages categorized as financial phishing includes phishing emails that involves financial organizations. |
| Employment Scam | E-mail messages categorized as employment scam includes emails like: bogus job offers, work from home scams, cash-handling scams, make money fast etc. |
| Investment Scam | E-mail messages categorized as investment scam includes emails like: penny stocks spam, pump and dump fraud, investment and pyramid schemes, investment seminars etc. |
| Financial Scam | E-mail messages categorized as financial scam includes emails like: fake online loans and grants, financial services, credit card scams, money lending, mortgage, private student loans etc. |
| Education Scam | E-mail messages categorized as education scam includes emails like: diploma/degree mill, illegitimate academic degrees, free education etc. |
| AdvanceFee Scam | E-mail messages categorized as advance fee scam includes scam emails like: Nigerian 419 and inheritance scams, unexpected money, up-front payment, advance-fee scams, reclaim scams, fake charities etc. |
| Lottery Scam | E-mail messages categorized as gambling scam includes emails like: gambling activities, casinos, betting etc. |
| Gambling Scam | E-mail messages categorized as gambling scam includes emails such as gambling activities, casinos, betting etc. |
| Dating Scam | E-mail messages categorized as dating scam includes emails like: online dating, bride scams, fake dating sites etc. |
| Adult Scam | E-mail messages categorized as adult scam includes scam emails like: mature/sexual content, porn, sex toys etc. |
| Pharma Scam | E-mail messages categorized as pharma scam includes emails like: diet and enhancement pills, miraculous remedies, narcotics, medical devices, online pharmacies etc. |
| Sales Scam | E-mail messages categorized as sales scam includes emails like: sales of email marketing lists, products, reports/webinars/conferences direct invitations, sellers and buyers scam, fraudulent orders etc. |
| Travel Scam | E-mail messages categorized as travel scam includes emails like: fake vacation rentals, free cruises, phony points rewards, rental scams etc. |
| Ecommerce Scam | E-mail messages categorized as ecommerce scam includes emails like: all kind of fake websites and online shops. |
| SPF Fail | SPF record lookup resulted in a *Fail* result. (*Phishing*) |
| SPF Soft fail | SPF record lookup resulted in a *Soft Fail* result. (*Potential Phishing*) |
| SPF Error | SPF record lookup failed. |
| SPF No record | Sender SPF record not found. |
| SPF Neutral | SPF record lookup resulted in a *Neutral* result. |
| SPF Pass | SPF record lookup resulted in a *Pass* result. |
| DKIM Invalid | DKIM signature is *Invalid*. (*Phishing*) |
| DKIM Error | DKIM signature failed to verify. |
| DKIM No signature | No DKIM signature present in the email. |
| Malicious URL | One or more URL(s) in the email were found malicious by the URL reputation check. |

### [MetaDefender Cloud Safe URL redirect](/docs/mdemail/6.4.2/operating/phishing-and-spam#metadefender-cloud-safe-url-redirect)

OPSWAT’s dynamic anti-phishing is a time-of-click analysis solution of URLs in email bodies.

If *Enable MetaDefender Cloud Safe URL redirect* is turned on under **Security Rules > [rule name] > Scan > Scan Email Body**, all links in the email body/bodies will be redirected through [MetaDefender.com](https://metadefender.opswat.com)[Safe URL redirect](https://onlinehelp.opswat.com/mdcloud/1._Safe_URL_redirect.html) service for URL reputation check.

If the URL turns out to be safe, then the browser is redirected to it immediately without any disruption of the browsing experience.

If the URL is detected as potentially malicious, then a warning screen calls the attention of the user to the possible risk:

### [Converting HTML emails to text-only](/docs/mdemail/6.4.2/operating/phishing-and-spam#converting-html-emails-to-text-only)

Hyperlinks and other, rich HTML features can be exploited to commit phishing, and other malicious attacks against the recipients of emails with HTML body.

As a counter-measure, Email Gateway Security supports converting emails with HTML body to text only emails.

To enforce the HTML body conversion to text only, the Deep CDR engine in MetaDefender Core needs to be configured to convert HTML to text.

Deep CDR is required

To use the HTML email to text-only conversion, the Deep CDR engine must be licensed, and the MetaDefender Core side Workflow rule – that is in use in the Email Gateway Security side Security Rule – must have Deep CDR enabled.

For details, see [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy) and [Configuration/Server profiles](/docs/mdemail/6.4.2/configuration/server-profiles).

## [Anti-spam](/docs/mdemail/6.4.2/operating/phishing-and-spam#anti-spam)

### [Classifications](/docs/mdemail/6.4.2/operating/phishing-and-spam#classifications)

The following classifications are applied to (potential) phishing emails:

- Spam
- Possible spam
- Anti-spam failure

For details see [Operating/Email classifications](/docs/mdemail/6.4.2/operating/email-classifications).

### [Handling of spam emails](/docs/mdemail/6.4.2/operating/phishing-and-spam#handling-of-spam-emails)

Based on the configuration, Email Gateway Security can handle (potential) spam emails in the following ways:

- Reject,
- Delete,
- Quarantine or
- Deliver.

For details see the *Anti-phishing and anti-spam* section under [Configuration/Policy](/docs/mdemail/6.4.2/configuration/policy).

## [Anti-Spam/Anti-Phishing diagnostics](/docs/mdemail/6.4.2/operating/phishing-and-spam#anti-spamanti-phishing-diagnostics)

Anti-spam verdict diagnostics is also displayed on the UI which makes it easier to report a false positive/negative verdict towards support. To see the processing history you need to navigate to **Audit > Email History** and select a specific email in the list.
