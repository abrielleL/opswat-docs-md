<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/data-trickling -->

# Data trickling

View as Markdown Ask ChatGPT about this page Ask Claude about this page Warning

Given by the nature of this setting, enabling data trickling may cause the ICAP Server to release potentially malicious content.

Always enable data trickling with care; only if you know what you are doing, if you are aware of the risk, and if you accept this risk.

Do not enable Data trickling then CDR/DLP is used, see [Deep CDR and Proactive DLP](/docs/mdicap/v5.15.0/operating/data-trickling#deep-cdr-and-proactive-dlp)

The problem

The Internet Content Adaption Protocol (ICAP) allows ICAP clients to pass HTTP messages to ICAP servers for some sort of transformation or other processing ("adaptation"). MetaDefender ICAP Server provides [ICAP](https://tools.ietf.org/html/rfc3507) interface on top of MetaDefender Core. When a user uploads data over HTTP (for example with a PUT or POST request), the contents of the request are forwarded to MetaDefender Core by MetaDefender ICAP Server for scanning. When a user downloads data from an external server (for example wit a GET request), the contents of the reply are also forwarded for scanning, before being sent to the user’s computer.

To be able to scan an HTTP request or response, the ICAP Server must have the whole content. It means that the ICAP Server must wait while all the contents arrive before it can start the scanning.

Moreover, before the ICAP server can have a verdict (whether the contents of the request or response are clean or infected), it must wait for the scan to complete.

Both to wait for the contents to arrive and to perform the scan may take for a long time, especially in case of huge files. As the request or response is blocked in the meantime, the end-user may have a bad downloading experience: she may think that the download stalled, or in extreme cases her download may even time out.

## [Solution: data trickling](/docs/mdicap/v5.15.0/operating/data-trickling#solution-data-trickling)

Data Trickling is designed to prevent the timeouts that can sometimes be associated with patience pages. To prevent such timeouts, data trickling trickles –or transmits at a very slow rate– bytes of the **original contents** –we call them drips – to the client at the beginning of the scan. Because the ICAP Server begins serving content without waiting for the scan result, timeouts do not occur. However, to maintain security, delivery of the full object can be withheld until the results of the content scan are complete (and the object is determined to not be infected).

The end-user will be able to download the already released drips. This can help to

1. Give a better downloading experience: the user will see download progress even while the ICAP Server is still processing;
2. Keep the browser session alive for huge files where the scanning may take long (even causing the download to time out).

Data trickling may start after a pre-configured delay, and with pre-configured drip size. As previously mentioned, it is also possible, to withhold the last portion of the contents for security considerations. For further details about configuring data trickling, see the *Data trickling* section in [4.2 Security Rules Policy](/docs/mdicap/v5.15.0/operating/security-rules-policy).

Warning

Trickling prefers usability to security

Data trickling is a usability feature that sacrifices security to provide better user experience in downloading, and to prevent long scans to cause timeouts.

## [How it works](/docs/mdicap/v5.15.0/operating/data-trickling#how-it-works)

For details about configuring data trickling, see the *Data trickling* section in [4.2 Security Rules Policy](/docs/mdicap/v5.15.0/operating/security-rules-policy).

1. The proxy forwards the contents of the request or the response to the ICAP Server.
2. The ICAP Server submits the contents to the Core. If trickling is enabled, then sets its timer to the FIRTS DRIP / DELAY.

   1. If the response from Core arrives before the timer elapses, then

      1. If the contents were allowed, then ICAP Server releases the contents that were returned by Core (see [602346555](/docs/mdicap/v5.15.0/operating/data-trickling#src-4864440)).
      2. If the contents were blocked, then the ICAP Server returns the block page (see [3.8 Customizing the block page](/docs/mdicap/v5.15.0/configuration/customizing-the-block-page)).
   2. If the response from Core does not arrive before the time elapses then

      1. If ENABLE TO WITHHOLD then

         1. If ENABLE TO WITHHOLD / SIZE would still remain after the drip, then

            1. The first drip is released in the pre-configured size;
            2. The timer is set to the ADDITIONAL DRIPS / DELAY.
         2. Else no drip is released, ICAP Server waits for the scan to complete.
      2. Else the drip is released
   3. If the response from Core does not arrive before the time elapses then

      1. If ENABLE TO WITHHOLD then

         1. If ENABLE TO WITHHOLD / SIZE would still remain after the drip, then

            1. The additional drop is released in the pre-configured size;
            2. The timer is set to the ADDITIONAL DRIPS / DELAY.
         2. Else no drip is released, ICAP Server waits for the scan to complete.
      2. Else the drip is released

Warning

If ENABLE TO WITHHOLD is not set, and the end of the file is reached any time during the trickling, then the whole original, potentially malicious content has been already released.

Always set ENABLE TO WITHHOLD, except only if you know what you are doing, if you are aware of the risk, and if you accept this risk.

5. If the scan completes, then:

- If the contents were allowed, then ICAP Server releases the contents that were returned by Core (see [602346555](/docs/mdicap/v5.15.0/operating/data-trickling#src-4864440)).
- If the contents were blocked, then ICAP Server aborts the connection.

Warning

After some drips have already been released, there is no way to cancel or call them back.

## [Limitations and drawbacks](/docs/mdicap/v5.15.0/operating/data-trickling#limitations-and-drawbacks)

### [Security](/docs/mdicap/v5.15.0/operating/data-trickling#security)

With data trickling enabled, the ICAP Server releases drips of the original contents, before the processing –e.g. anti-malware scanning– completes. These drips being part of the original contents, may contain malicious code.

As a consequence, with data trickling enabled, the risk –that malicious content reaches the end-user or the upload server– is much higher.

Warning

Given by the nature of this setting, enabling data trickling may cause the ICAP Server to release potentially malicious content.

Always enable data trickling with care; only if you know what you are doing, if you are aware of the risk, and if you accept this risk.

#### [Partial content](/docs/mdicap/v5.15.0/operating/data-trickling#partial-content)

Warning

All major browsers are capable to handle partial downloads and support to automatically retry previously failed, incomplete downloads. In these cases it is very common to request only the missing part of the content using [range requests](https://tools.ietf.org/html/rfc7233). As with trickling ICAP Server releases drips of the original content, the risk is even higher that range requests will be in use and malicious content may finally be downloaded.

For further details see: [4.8 Risks with range request](/docs/mdicap/v5.15.0/operating/risks-with-range-request).

### [Block page](/docs/mdicap/v5.15.0/operating/data-trickling#block-page)

Warning

After some drips have already been released, there is no way to cancel or call them back.

After the trickling has already been started, there is no point in serving the block page. The reason for that is that the block page would be broken caused by the already released original content.

### [Deep CDR and Proactive DLP](/docs/mdicap/v5.15.0/operating/data-trickling#deep-cdr-and-proactive-dlp)

Warning

After some drips have already been released, there is no way to cancel or call them back.

After the trickling has already been started, there is no point in serving contents that have been processed by Core (e.g. sanitized files by Deep CDR or processed files by Proactive DLP). The reason for that is that the processed contents would be broken caused by the already released original content.

Info

A potential resolution may be to choose a FIRST DRIP / DELAY value carefully so that reasonable contents can still finish processing before the first drip is released.

Info

An other potential solution may be to apply trickling to certain ICAP Server workflows only. Applying filters to workflow, you can select content types (e.g. configuring the Content-Type header as a filter), where data trickling may not be allowed, thus making content processing (CDR, redaction, metadata removal, etc.) usable.

###### [Example](/docs/mdicap/v5.15.0/operating/data-trickling#example)

The following filter will match PDF files (by the content type). Disabling data trickling for this workflow can make Deep CDR and/or Proactive DLP usable for PDF files.

For a reference of MIME types of certain content types see <https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/MIME_types/Complete_list_of_MIME_types>.
