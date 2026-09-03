<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/is-metadefender-core-affected-by-nginx-cves- -->

# Is MetaDefender Core affected by NGINX CVEs?

- This article applies to MetaDefender Core prior to 5.18.0
## [**Issue**](/docs/mdcore/v5.21.0/knowledge-base/is-metadefender-core-affected-by-nginx-cves-#issue)

### [Impact assessment for six NGINX vulnerabilities against MetaDefender Core:](/docs/mdcore/v5.21.0/knowledge-base/is-metadefender-core-affected-by-nginx-cves-#impact-assessment-for-six-nginx-vulnerabilities-against-metadefender-core)

- CVE-2026-42945: Not affected. MD Core’s rewrite rules do not use nested or overlapping capture groups, capture substitutions such as $1/$2, or the vulnerable rewrite patterns described in the advisory.
- CVE-2026-42946: Not affected. MD Core does not use the scgi_pass or uwsgi_pass modules in the NGINX configuration.
- CVE-2026-40460: Not affected. MD Core does not use the HTTP/3 QUIC module.
- CVE-2026-42926: Not affected. The NGINX configuration does not use proxy_http_version 2.
- CVE-2026-40701: Low risk. The vulnerability only affects deployments using specific mTLS and OCSP validation settings in NGINX. Please verify whether ssl_verify_client on|optional and ssl_ocsp on are enabled in the active NGINX configuration.
- CVE-2026-42934: Not affected. The vulnerable configuration combination (charset/source_charset/charset_map together with proxy_pass and proxy_buffering off) is not used in the NGINX configuration.

## [**Resolution**](/docs/mdcore/v5.21.0/knowledge-base/is-metadefender-core-affected-by-nginx-cves-#resolution)

- Upgrade to MetaDefender Core 5.19.0 or later for NGINX 1.30.1.
- If you must stay on 5.18.0 temporarily, please log a support case

Support:

If you require further assistance, please follow these instructions on [How to Create Support Package?](https://www.opswat.com/docs/mdcore/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/support).
