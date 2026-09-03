<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module -->

# Ometascan NGINX module Release Notes

## [Version 1.5.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-150)

Release date: May 8, 2026

Enhancement and new features:

- Support active and passive health check

## [Version 1.4.1](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-141)

Release date: Sep 12, 2025

Enhancement and new features:

- Support NGINX plus R34
- Support integrate with OIDC NGINX Plus module

## [Version 1.4.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-140)

Release date: Dec 10, 2024

Enhancement and new features:

- Support NGINX plus R33
- Add new directive **ometascan_set_header** (refer to [Directives](/docs/mdicap/v5.14.1/integrations/nginx-integration-module#directives)) to help add custom header into HTTP request (a simple way to add X-MDCLOUD-APIKEY for using ICAP Cloud with NGINX)

## [Version 1.3.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-130)

Release date: Jul 09, 2024

Enhancement and new features:

- Support HTTP2
- Support NGINX plus R32

## [Version 1.2.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-120)

Release date: Dec 26, 2023

Enhancement and new features:

- Support chunked transfer-encoding requests to allow bad requests (MetaDefender ICAP Server 5.4.0+ is required)
- New option to allow bad requests, see more at [NGINX Integration Module](/docs/mdicap/v5.14.1/integrations/nginx-integration-module) (using `ometascan_allow_bad_request_traffic` option)
- Deprecate directive `ometascan`*_*`pre_cache_ size`
- Support URL redirect for block page configuration (MetaDefender ICAP Server 5.4.0+ is required)

Fixed issues:

- Request will be hang if enable both ometascan_pre___cache and app_protect___enable (by default ometascan_pre___cache is off)

## [Version 1.1.1](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-111)

Release date: Sep 19, 2023

Fixed issues:

- Ometascan NGINX module is crashed incase bad request and error_page is configured in nginx.conf

## [Version 1.1.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-110)

Release date: Sep 11, 2023

Enhancement and new features:

- Support integrate with App Protec

Fixed issues:

- Ometascan NGINX module is crashed if handle the bad request
- ometascan_ssl_session_reuse does not take affect

## [Version 1.0.0](/docs/mdicap/v5.14.1/release-notes/changelog-ometascan-nginx-module#version-100)

Release date: Nov 21, 2022

First rollout Ometascan NGINX module
