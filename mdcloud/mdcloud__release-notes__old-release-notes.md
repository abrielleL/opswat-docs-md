<!-- source: https://www.opswat.com/docs/mdcloud/release-notes/old-release-notes -->

# Old release notes

## [November 10, 2021](/docs/mdcloud/release-notes/old-release-notes#november-10-2021)

**New Features / Updates**

- Notifications and Alerts allows admins of organizations to get notified via email or in app for.

  - users added to the organization
  - users removed from the organization
  - user role changes
  - access attempts outside the IP allowlist
  - when certain % thresholds of daily API limits are reached

**Bugs / Fixes**

- The rescan API has been disabled
- The limits/status endpoint now returns organization level limits (instead of account level limits) for those who are part of an organization
- Updates to our [licensing table](https://metadefender.opswat.com/licensing)
- Fixed scan history pages (before only would show one page even if there were multiple)
- Fixed username dropdown menu on metadefender.opswat.com

## [October 19, 2021](/docs/mdcloud/release-notes/old-release-notes#october-19-2021)

**Bugs / Fixes**

- Resolved issue with main header when scrolling
- Fixed issue with Mitre Att&ck UI in dynamic analysis

## [September 16, 2021](/docs/mdcloud/release-notes/old-release-notes#september-16-2021)

**New Features / Updates**

- Improved scan times for commercial and enterprise customers

**Bugs / Fixes**

- Resolved issue with v4/apikey/limits endpoint not updating correctly
- Updated number of commercial engines on licensing page to reflect current agreements

## [August 17, 2021](/docs/mdcloud/release-notes/old-release-notes#august-17-2021)

**New Features / Updates**

- Dashboard and Statistics pages on MD Cloud UI which allows users to visually track...

  - Allowed and blocked files
  - Deep CDR of files
  - Vulnerabilities

**Bugs / Fixes**

- Fixed issue with organization level limits
- Improved translations on Japanese version of MD Cloud site

## [July 16, 2021](/docs/mdcloud/release-notes/old-release-notes#july-16-2021)

**New Features / Updates**

- Increased number of files in archive to 1000
- mTLS authentication for enterprise customers

**Bugs / Fixes**

- v4/status/engines-cloud endpoint updated to reflect current engines
- multiscanning enabled by default

## [Jun 30, 2021](/docs/mdcloud/release-notes/old-release-notes#jun-30-2021)

**New features / update:**

- Added support for [organization account](/docs/mdcloud/account-management/accounts--organization)
- Added support for [IP allowlisting](https://www.opswat.com/docs/mdcloud/account-management/accounts--organization)
- Added support for BYOI (bring your own identity) (applicable to [Enterprise licensing](https://metadefender.opswat.com/licensing))
- Added support for Mutual TLS authentication (applicable to [Enterprise licensing](https://metadefender.opswat.com/licensing))
- Increased maximum number of files per archive (applicable to [Commercial licensing](https://metadefender.opswat.com/licensing))

## [May 19, 2021](/docs/mdcloud/release-notes/old-release-notes#may-19-2021)

**New features / update:**

- Added Avira engine to commercial licensing

## [Apr 14, 2021](/docs/mdcloud/release-notes/old-release-notes#apr-14-2021)

**Fixed Issues:**

- Token mismatch error on newly created API key
- Safe redirect error with anonymous user
- Outdated Leaderboard

## [Mar 4, 2021](/docs/mdcloud/release-notes/old-release-notes#mar-4-2021)

**New features / update:**

- Anonymous users now have smaller limits:

  - Prevention API 3 (previous 40)
  - Reputation API 500 (previous 4000)
- Registered users still have the same limits as before
- Introduced shared rate-limiting for organizations
- Introduced support for the following file types in Deep CDR: OTT, ODS, OTS, ODP, OTP
- Decoupled CDR from multiscanning: now users are able to sanitize a file without performing multiscanning
- The “rule: sanitize” header has been deprecated in favor of “rule: cdr”. When rule is used with “cdr”, it will not also perform multiscanning unless requested, whereas “sanitize” will automatically perform multiscanning as well

**Fixed Issues:**

- Fixed an error with webhooks crashing when using private processing
- Improved rendering of long names for mobile displays
- Improved response format when multiscanning is disabled

## [Feb 5, 2021](/docs/mdcloud/release-notes/old-release-notes#feb-5-2021)

**New features / update:**

- The uploaded archives now consume limits based on files inside the archive

**Fixed Issues:**

- Removed unnecessary fields when multiscanning is not performed
- The “file_info.upload_timestamp” was not showing the exact time when the file was uploaded
- The cache was not cleared after private files were deleted
- Throw an error when uploading archives with sandbox header
- Newly uploaded files were showing a message saying “we have a newer analysis for this file”
- Fixed several page crashes issues

## [Jan 20, 2021](/docs/mdcloud/release-notes/old-release-notes#jan-20-2021)

**New features / update:**

- The Sandbox results now display separate tabs for each OS version along with a detailed summary:

- Decoupled multiscanning from sandbox: now sandbox analysis can be performed without static analysis

**Fixed Issues:**

- The Filename is now trimmed when longer than 256 characters in multipart uploads
- X-Content-Type-Options set to 'nosniff'
- Improved browser caching mechanism using the Cache-control header
- Allow access to the billing portal for paid users who don’t have an active subscription
- Improved error messaging when users run out of limits to specify which limit was exceeded on error

## [Dec 22, 2020](/docs/mdcloud/release-notes/old-release-notes#dec-22-2020)

**New features / update:**

- Added URL classification:

- Added Mitre att&ck UI for dynamic analysis:

- Added a banner on the frontend announcing a pricing increase
- Added a new endpoint to delete the sanitized version of files from our servers on request [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Delete the sanitized version of the file)

**Fixed Issues:**

- Hide scan history page if no data is available in the UI
- Enhanced error detection in safe redirect
- Fixed certain cases when EXIF metadata was not generated when uploading images

## [Dec 8, 2020](/docs/mdcloud/release-notes/old-release-notes#dec-8-2020)

**New features / update:**

- Released a new customer portal integrated with Stripe: now it is possible to update payment information and billing details. Canceling subscriptions and billing details have also moved to the Stripe portal.
- Added imphash on the scan results overview page

**Fixed Issues:**

- Added the OS on which the dynamic analysis was performed to the results JSON
- Fixed an issue with bulk hash lookups returning duplicate entries
- Improved priority for commercial sandbox users

## [Nov 24, 2020](/docs/mdcloud/release-notes/old-release-notes#nov-24-2020)

**New features / update:**

- We have introduced a progress percentage for Sandbox scanning in the UI and API
- Improved Deep CDR report filter dropdown usability

**Fixed Issues**

- Added sanitized file report link to the summary page since there was no way to navigate to that report in the UI
- Improved error messaging
- Improved integration with OPSWAT SSO

## [Oct 21, 2020](/docs/mdcloud/release-notes/old-release-notes#oct-21-2020)

**Fixed Issues:**

- Enhanced network connectivity for dynamic analysis & improved timeout
- Enhanced peinfo error handling
- Safe redirect apikey was sometimes not created
- Fixed some cases when the Deep CDR option was not available for rescan in the UI
- Added scan time to dynamic analysis report

## [Oct 14, 2020](/docs/mdcloud/release-notes/old-release-notes#oct-14-2020)

**New features / update:**

- Added new options for sandbox processing: now users have the ability to select the browser and timeout
- The UI now accepts archive passwords for scanning archives

**Fixed Issues:**

- On the first visit, reports are cached for 15 minutes
- Homepage design updates
- Archive parent link on the scan results page now points to extracted files
- Added Open graph image tag to improve the Facebook sharing experience
- Sandbox empty sections are now filtered out
- Added new failed to scan status for IP/Domain

## [Sep 2, 2020](/docs/mdcloud/release-notes/old-release-notes#sep-2-2020)

**Fixed Issues:**

- Extended website support for older browsers
- Updates NPS banner display and positioning
- UX updates for “Analyze again” buttons and Dynamic Analysis edge cases

## [Aug 13, 2020](/docs/mdcloud/release-notes/old-release-notes#aug-13-2020)

**New Features:**

- Added a new engine to Multiscanning: Webroot
- Added “Analysis API” to our online store and increased price for higher tiers of “Prevention API”
- Dynamic Analysis summary page UI updates
- Added an NPS banner for logged in users
- Add community forum link in the footer and dropdown menu
- Added additional background images to the homepage

**Fixed Issues:**

- Fixed a Deep CDR page crash
- Added a graceful fail for invalid data on the Sandbox card
- Fixed extracted files results status when failing
- Fixed history graph display issue
- Added shim for requestAnimationFrame to enable mobile users with opera mini to view the homepage without an error.

## [Jul 24, 2020](/docs/mdcloud/release-notes/old-release-notes#jul-24-2020)

**New Features:**

- Sandbox dynamic analysis has now exited the beta state. It’s API is stable, the infrastructure is scalable and highly available, and is commercially available

**Fixed Issues**

- Updated ToS URL
- UI polishing
- Fixed issues with invalid apikeys after logout
- Improved Safe URL redirect URL handling
- Updated license processing for apikeys expiring the current day
- Fixed an issue with online store emails ignoring discount codes

## [Jul 9, 2020](/docs/mdcloud/release-notes/old-release-notes#jul-9-2020)

**New Features:**

- UI updates:

  - Unify homepages by removing Deep Blue and Show themes, and updating the City theme
  - Updated cookie banner design
  - Enhanced notifications system
  - Update drop file banner design
  - Enhanced menu
  - Update scan component advanced options design
  - Added better visual for the community page when a file has no votes

**Fixed Issues**

- Updated page titles and descriptions for better SEO ranking
- Fix manifest file image path
- Fix Package Efficacy image logos
- Added a scan history badge on the scan results menu
- Update Licensing page FAQ
- Improve the translations process by implementing a key scanner.

## [June 25, 2020](/docs/mdcloud/release-notes/old-release-notes#june-25-2020)

**New Features:**

- Added sandbox support for multiple files, including full support for Microsoft Office suite, python scripts and windows executables
- Added a new endpoint for retrieving the full list of engines: [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Engine definitions)

**Fixed Issues:**

- Improved notification messaging on the UI:

  - Info note to a user when uploading an infected file eligible for gamification points
  - Info message for clean archives with infected files inside
  - Banner informing the user that a newer result exists
- Integrated a service for application monitoring and error tracking in the frontend
- Updated File Overview to show the data as soon as it’s available
- Added Beta tag to the Dynamic Analysis page menu entry
- Added a general error handler at the app root to fail gracefully
- Updated EXIF table responsive design
- Fixed status page notification to show only Metadefender Cloud issues
- Fixed CDR report links to “before CDR” results
- Added Rate limit error message for guests users when the limit is reached
- Updated clickable area for headers in the Dynamic Analysis page
- Improved status description for dynamic analysis
- Added link to the chrome extension page in the footer
- Fixed manifest file URL.
- Fixed homepage background zoom issue on mobile

## [June 11, 2020](/docs/mdcloud/release-notes/old-release-notes#june-11-2020)

**New Features:**

- New UI/UX for the IP-Domain scan results pages:

- New UI/UX for the dynamic analysis page:

**Fixed Issues:**

- Improved the online store UI to reflect the current subscription if present
- Updates to forms displayed on the market share report

## [May 27, 2020](/docs/mdcloud/release-notes/old-release-notes#may-27-2020)

**New Features:**

- New UI/UX scan results pages

  - Data sanitization shows actions performed

- The rescan button now allows specifying what operations to perform on the file

- New API endpoint for retrieving file scan history for an apikey:

  - [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Apikey scan history)

**Fixed Issues:**

- Fixed filetype detection for adobe illustrator files and PDF
- Improved analyze again validation
- Deprecate threat intelligence top hashes feed
- Enhances to automatic payment workflow on our online store

## [Version 4.8.0](/docs/mdcloud/release-notes/old-release-notes#version-480)

Release date: Dec 24th, 2019

**New features:**

- **Bitdefender joins Commercial Cloud!**
- New UI for leaderboard and licensing page
- Added new scan result [Public APIs](/integrations/public-apis#Description on scan result codes): PUA (22) and unsupported application (23)

**Fixed issues:**

- added a default filename with correct extension to the sanitized version of files uploaded without a filename
- "Microsoft Defender ATP" engine was renamed to "Windows Defender"
- Fixed infinite scroll on the account page

## [Version 4.7.0](/docs/mdcloud/release-notes/old-release-notes#version-470)

Release date: Dec 5th, 2019

**New features:**

- **McAfee joins Commercial Cloud!** The well-known engine is now part of our [commercial](https://metadefender.opswat.com/licensing) engines offering for paid customers.
- New account [page](https://metadefender.opswat.com/account): we are continuing our website update process with an update to the UI and UX of the account page. We additionally added more usage charts for Sandbox analysis, Domains and URL lookups, as well as merging the coupon page into the account page.

**Fixed issues:**

- Enhanced file type extension detection
- Fixes for use cases where files never finish scanning
- Optimizations for autoscaling capacity based on traffic
- Localization updates
- UI polishing

## [Version 4.6.5](/docs/mdcloud/release-notes/old-release-notes#version-465)

Release date: 14 November 2019

**Fixed Issues:**

- Fixed rescanning for files sent with invalid scan rules
- Enhanced scanning to reduce the number of timeouts for files
- Improved error messages
- UI fixes

## [Version 4.6.0](/docs/mdcloud/release-notes/old-release-notes#version-460)

Release date: 23 October 2019

**New Features:**

- Threat intelligence feed allowlist: a new addition to our Threat Intelligence family of feeds, the "Latest Allowlist Feed". Gain instant access to the latest hashes detected as clean by our multiscanning engines and add them to your organization's allowlist. The feed can be queried up to 1 year in the past, and filtered based on file category. Read more here: [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Latest clean hashes).

**Fixed Issues:**

- Lots of fixes to our new homepages
- Fixed several backward compatibilities redirect issues
- Improvements for scan performance

## [Version 4.5.0](/docs/mdcloud/release-notes/old-release-notes#version-450)

Release date: 30 September 2019

**New features:**

- OPSWAT Threat Name: to make it easier for users to understand the nature of threats without having to evaluate dozens of different threat names generated by anti-malware engines, each with its unique format, OPSWAT has introduced a general "threat_name" field. This field can be seen:

  - in the latest infected hashes ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Latest Infected Hashes)) all the infected hashes from the feed will have an associated threat name
  - when doing lookups by hash ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Hash lookup)) or by data ID ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Fetch analysis result)) all the new file scans will have this property from now on. It is also visible in the UI under the SHA256 property

- Free user limit increase: because of popular demand we are increasing the limit of Prevention API for our free users from 40 to 100 requests per day. This allows our community to submit more files to be analyzed and sanitized, or request rescanning of files. Happy scanning!

## [Version 4.4.6](/docs/mdcloud/release-notes/old-release-notes#version-446)

Release date: 5 September 2019

**Fixed issues:**

- Fixed file sanitization download issues
- Updates to malware sharing partner program
- Performance improvements

## [Version 4.4.3](/docs/mdcloud/release-notes/old-release-notes#version-443)

Release date: 13 August 2019

**Fixed issues:**

- Added a new "In queue" status to better reflect file processing
- Fixed issues when sanitized filename wasn't always correct
- Improved IP/URL reputation sources
- Outbreak report now includes a dropdown to review previous reports

## [Version 4.4.0](/docs/mdcloud/release-notes/old-release-notes#version-440)

Release date: 24 July 2019

**New features:**

- Introducing a new feed for reading the latest infected hashes ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Latest Infected Hashes)). Exposing infections in real-time as they are scanned, this new feed offers different options for filtering hashes based on the file type and date scanned. The free version of the feed offers access to the first 1000 hashes each day.

**Fixed issues:**

- Added sha1 to the file upload response for checking if the file upload was done correctly
- Fixed issues when the scan results progress percentage was 100% but the scan result code was 255
- Added the option to undo a vote on a hash
- Removed unnecessary fields from file upload response

## [Version 4.3.0](/docs/mdcloud/release-notes/old-release-notes#version-430)

Release date: 19 June 2019

**New Features:**

- Safe URL redirect: Browsing the web has just become safer with our new safe URL redirect feature. Your product can now replace all URLs with MetaDefender Cloud safe URLs for a fast and safe web browsing experience. Start preventing browser-based attacks today! See our documentation for more [details](https://www.opswat.com/docs/mdcloud/operation/safe-url-redirect).

**Fixed issues:**

- The threat intelligence feed can now be queried based on categories
- The month dropdown from the market share report and the leaderboards now changes the URL
- Enhanced file type extension detection
- Fixes to scan results information

## [Version 4.2.0](/docs/mdcloud/release-notes/old-release-notes#version-420)

Release date: 30 May 2019

**New Features:**

- Multi-region cloud: starting this version, our cloud is hosted in an additional region besides North America: Europe central. This means not only that the speed of the API requests will improve for our users in Europe, but also that their data will not leave the continent (files will be uploaded, hosted and scanned within the European continent). This feature is enabled by default via DNS geo-load balancing.
- We have added a navigation dropdown to our leaderboards. Now users can view previous versions of leaderboards and compare rankings.

**Fixed issues:**

- Fixed spacing and alignment issues generated by Japanese translations.
- File uploads now also return the sha256 checksum (helpful for verifying that the file was uploaded correctly)
- Enhanced code snippets

## [Version 4.1.0](/docs/mdcloud/release-notes/old-release-notes#version-410)

Release date: 8 May 2019

**New Features:**

- Multi-language support: this release of MetaDefender Cloud brings support for multiple languages, the first language added is Japanese. More languages will be added in the future.

- New leaderboard: users with the most votes will now be part of our new [Top Voters](https://metadefender.opswat.com/leaderboard#!/voters/) leaderboard.

**Fixed Issues:**

- Enhanced sanitization error: all files which have failed to sanitize will have additional information displayed in the UI
- Updated all code snippets to v4 API
- Added extra descriptions for multiple sections in the website
- Fixed reputation points notifications not being displayed
- Package efficacy report form was not loading

## [Version 4.0.0](/docs/mdcloud/release-notes/old-release-notes#version-400)

Release date: 10 Apr 2019

**New Features:**

- Callback URL: With this version, there is an alternate way of scanning files besides long polling by data_id. Users can now send a "callbackurl" webhook where we will POST the results once scanning is finished, making reading the scan results more lightweight on the client side. Please see the documentation: [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Analyze file).
- Market Share Report navigation: navigating through our different [Market Share Reports](https://metadefender.opswat.com/reports/anti-malware-market-share#!/) can now be done using the dropdown menu:

- Official switch to V4: we have recently [announced](http://www.opswat.com/blog/metadefender-cloud-3-77-0-released) the release of our V4 API. Now we are officially changing the API version to 4.0.0 to reflect the API change. Checking the API version can be done via the version endpoint (see here for more: [MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#API version)).
- We have increased the sandbox limit for registered users: non-registered users continue to have a limit of 1 dynamic analysis per day, while registered users will be able to perform 5 dynamic analysis per day for free.

**Fixed issues:**

- Improved error handling for limit reached
- The leaderboard has been updated to only show 1 point for each submission instead of 5 points
- Better handling of file scans sent by URL ("downloadfrom" header)

## [Version 3.77.0](/docs/mdcloud/release-notes/old-release-notes#version-3770)

Release date: 8 Mar 2019

**New Features:**

- Android Info: APK files uploaded are now analyzed and the Manifest metadata is now stored and displayed in the UI. This is info is also available via the API ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#APK manifest lookup)).

- V4 API: The latest version of our API, designed with modularity in mind, and compatible with MetaDefender API. See [6. V4 API](/docs/mdcloud/integrations/v4-api) for details.

**Fixed issues:**

- User activity history was missing frontend activity

## [Version 3.76.0](/docs/mdcloud/release-notes/old-release-notes#version-3760)

Release date: 22 Feb 2019

**New Features:**

- The first beta release of Dynamic Analysis:

**Fixed issues:**

- Removed duplicates in file scan history
- Performance improvements for hash lookup
- In certain cases, the throttling message was not displayed

## [Version 3.75.0](/docs/mdcloud/release-notes/old-release-notes#version-3750)

Release date: 18 Jan 2019

**New features:**

- We added 2 new engines to our free offering: Baidu and Jiangmin, reaching a total of 37 engines.
- File Exif and Portable Executable information (peinfo) have been moved to the "File information" tab
- We simplified our vulnerability submission process, to make it easier to report vulnerabilities:

**Fixed issues:**

- Rescanning of older files is now working
- Improved error handling on the frontend
- Updated [leaderboard](https://metadefender.opswat.com/leaderboard) generation
- Removed old threat intelligence page in favor of <https://www.opswat.com/developers/threat-intelligence-feed>
- Removed old IP documentation page in favor of [Analyzing IPs with MetaDefender Cloud](/docs/mdcloud/operation/analyzing-ips-with-metadefender-cloud)

## [Version 3.74.0](/docs/mdcloud/release-notes/old-release-notes#version-3740)

Release date: 27 Dec 2018

**New features:**

- URL scanning ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#URL lookup)) and Domain scanning ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Domain lookup))were released, and added as search options in our multi search bar
- Repository scanning ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#Scanning a repository)): a single API call scan a git repository from one of the supported vendors: Github, Bitbucket or Gitlab.
- File badge ([MetaDefender Cloud API v4](/v-4/metadefender-cloud-api-v4/ref#File badge)): display a badge showing the scan results of a hash on any website
- Popup to remind the users to update their automatically generated nicknames
- We created a [Leaderboard](https://metadefender.opswat.com/leaderboard#!/) to promote our monthly most active malware contributors.

**Fixed issues:**

- Default nickname format update
- Market Share Report data is now loading from CDN
- Improved the display of scan results for clean archives with infected files attached
- Added throttling for URL and domain bulk lookups
