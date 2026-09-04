<!-- source: https://www.opswat.com/docs/macloud-sdp/release-notes/sdp-gateway -->

# SDP Gateway

## [SDP Gateway 1.6.13 - May 20, 2025](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-1613---may-20-2025)

1. New features:

   - Support exporting logs to SYSLOG server.
2. Bugs fixed:

   - Handle big log files gracefully by improving the log rotating mechanism.
3. Known issues:

   - Upgrade feature may not work. A workaround is to download a new OVA/XVA and redeploy.

## [SDP Gateway 1.6.12 - February 26, 2025](/docs/macloud-sdp/release-notes/sdp-gateway#sdp--gateway-1612---february-26-2025)

1. Bugs fixed:

   - High disk usage.
2. Known issues:

   - Upgrade feature may not work. A workaround is to download a new OVA/XVA and redeploy.

## [SDP Gateway 1.6.11 - November 27, 2024](/docs/macloud-sdp/release-notes/sdp-gateway#sdp--gateway-1611---november-27-2024)

1. Bugs fixed:

   - CPU soft lockup.
2. Known issues:

   - Upgrade feature may not work. A workaround is to download a new OVA/XVA and redeploy.

## [SDP Gateway 1.6.10 - September 13, 2024](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-1610---september-13-2024)

1. Enhancements:

   - Replace AWS IAM user with IAM roles anywhere.
2. Bugs fixed:

   - Update SSH dependency with critical CVE.
3. Known issues:

   - Upgrade feature may not work. A workaround is to download a new OVA/XVA and redeploy.

## [SDP Gateway 1.6.9 - June 12, 2024](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-169---june-12-2024)

1. Enhancements:

   - Product rebranding from "OPSWAT MetaAccess SDP" to "OPSWAT MetaDefender IT Access"

## [SDP Gateway 1.6.8 - November 21, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-168---november-21-2023)

1. Enhancements:

   - MA API endpoint to export gateway session's network traffic (bytes sent, bytes received) to csv file
   - MA API endpoint to update list SDP gateway session bandwidth
2. Bugs fixed:

   - Increase timeout before the client and GW drop connections

## [SDP Gateway 1.6.7 - September 20, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-167---september-20-2023)

1. Bugs fixed:

   - Fix issues related to write log service

## [SDP Gateway 1.6.6 - August 16, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-166---august-16-2023)

1. Bugs fixed:

   - Login screen issue on GW 1.6.5
   - Gateways being detected as 'out-of-date' when they are the most recent released version

## [SDP Gateway 1.6.5 - July 15, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-165---july-15-2023)

1. Bugs fixed:

   - Gateways being detected as 'out-of-date' when they are the most recent released version

## [SDP Gateway 1.6.4 - June 6, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-164---june-6-2023)

1. Bugs fixed:

   - The debug logs are still persistent without enabling the debug flag
   - Build SDP gateway failed

## [SDP Gateway 1.6.3 - March 21, 2023](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-163---march-21-2023)

1. Enhancements:

   - Improve performance during client connections
2. Bugs fixed:

   - Mac SDP OWC integration needs updating for how to get gateway pools
   - Live access updates fail if gateway lookup fails

## [SDP Gateway 1.6.1 - September 20, 2022](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-161---september-20-2022)

1. Enhancements:

   - Allow administrators to push software updates to SDP Gateways
   - SDP Gateways can self-update to newer software versions
   - New event logs for SDP Gateway update

## [SDP Gateway 1.5.8 - March 15, 2022](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-158---march-15-2022)

1. Bugs fixed:

   - VPN | Ping retries exceed 15 seconds
   - Gateway should not send DNS updates when there is no delta
   - Implement buffered debug logging for gateways
   - Spike | Connection samples reported from gateways can sometimes have the connIpTableState field missing

## [SDP Gateway 1.5.7 - February 15, 2022](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-157---february-15-2022)

1. Enhancements:

   - Gateways still using impulse.com domains
2. Bugs fixed:

   - Spike | Private Gateway fails to log in if done so quickly after boot

## [SDP Gateway 1.5.6 - January 18, 2022](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-156---january-18-2022)

1. Enhancements:

   - Private gateway iptables server is failing to respect large payloads, need to increase limit
2. Bugs fixed:

   - Private Gateway fails to read userData correctly-- fails deployment across all stages
   - Gateways still using impulse.com domains

## [SDP Gateway 1.5.5 - December 21, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-155---december-21-2021)

1. Enhancements:

   - Use standard ec2-user account for AWS Private Gateways
2. Bugs fixed:

   - Host logs from PG deployed to AWS are not being published to CloudWatch

## [SDP Gateway 1.5.4 - November 16, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-154---november-16-2021)

1. Bugs fixed:

   - Cloud gateways don't register against their local region controller
   - Connections that transition from established to closed state quickly have a high probability of not being tracked

## [SDP Gateway 1.5.3 - October 19, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-153---october-19-2021)

1. New features:

   - Display the log stream ID easily for helping troubleshoot Gateway
   - Allow admins to select which stage (US vs EU) to register a Gateway
2. Enhancements:

   - Updates to consolidate logging to CloudWatch
   - Expand LogRotate
3. Bugs fixed:

   - Update ssh2 dependency with critical CVE
   - Update morgan dependency with critical CVE
   - Update cryptiles dependency with critical CVE
   - Correctly disallow SSH to Private Gateways
   - Fix bug possibly pulling the wrong container versions at gateway boot
   - Fix docker container restart issue in initialization

## [SDP Gateway 1.5.2 - September 21, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-152---september-21-2021)

1. Enhancements:

   - Improve performance during client connections
2. Bugs fixed:

   - Detect “0.0.0.0” as an invalid DNS server configuration and ignore it
   - Fix bug allowing gateways to pull unexpected docker image version

## [SDP Gateway 1.5.1 - August 24, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-151---august-24-2021)

1. Enhancements:

   - Disconnect all users on the account when “Enable SDP Gateways” is changed to false
   - Disconnect any connected SDP session when a client device is reassigned to a different group, when a different SDP Gateway Pool is used on the new group
2. Bugs fixed:

   - Fix bug to disconnect SDP sessions when the “default” gateway pool is changed resulting in a new gateway assigned to devices
   - Fix a bug tracking network usage on the Gateway

## [SDP Gateway 1.5.0 - July 27, 2021](/docs/macloud-sdp/release-notes/sdp-gateway#sdp-gateway-150---july-27-2021)

1. Admins can now deploy a SDP private gateway from the Microsoft Azure marketplace to protect applications/resources via SDP.
2. Enhancements

   - Performance improvement for terminating multiple sessions on a gateway
   - Improve IP discovery through load-balanced networks to improve changes of hole-punching success
3. Bugs fixed:

   - An input was duplicated when a user tried the second time
