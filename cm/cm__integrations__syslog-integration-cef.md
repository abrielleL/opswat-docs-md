<!-- source: https://www.opswat.com/docs/cm/integrations/syslog-integration-cef -->

# Syslog Integration – CEF (Common Event Format)

## 1. Overview

My OPSWAT Central Management (MOCM) supports sending log messages to local or remote Syslog servers using **CEF (Common Event Format)**.

CEF is a text-based log format developed by ArcSight™ and widely used by SIEM solutions. It uses **Syslog** as the transport mechanism. A CEF message consists of:

- An optional **Syslog header (prefix)**
- A **CEF header**
- A **CEF extension** (key–value pairs)

> **Warning**
>
> In some environments, the Syslog header may be omitted and only the CEF payload is sent

## 2. CEF Message Structure

```javascript
CEF:Version|Device Vendor|Device Product|Device Version|Device Event Class ID|Name|Severity|Extension
```

### CEF Header Fields

| Field | Required | Description |
| ---- | ---- | ---- |
| Version | Yes | CEF version. Current value is always `0`. |
| Device Vendor | Yes | `OPSWAT` |
| Device Product | Yes | `MOCM` (My OPSWAT Central Management) |
| Device Version | Yes | MOCM version |
| Device Event Class ID (Signature ID) | Yes | Combined from `EventType` and `Type` |
| Name | Yes | Human-readable event name |
| Severity | Yes | Event severity from `0` to `10` (INFO events use `2`) |
| Extension | No | Additional key–value data |

## 3. Event Categories and Mapping

### 3.1 Device Events (MD Endpoint)

| Event Class ID | Description |
| ---- | ---- |
| `device_events.added` | Device added |
| `device_events.critical_issue_found` | Device reported critical issues |
| `device_events.issue_cleared` | Device changed status to compliant |
| `device_events.unexempt_device` | Device unexempted |
| `device_events.deleted` | Device removed by administrator |
| `device_events.unseen_removed` | Device deleted by unseen setting |
| `device_events.infection_found` | Device reported threats violate by policy |
| `device_events.unknown_device_detected` | Device Unknown |
| `device_events.issue_found` | Device changed status to non-compliant |
| `device_events.critical_issue_clear` | Device reported no more critical issues |
| `device_events.in_grace_period` | Entered the grace period |
| `device_events.not_in_grace_period` | Ended the grace period |
| `device_events.report_no_threat` | Device threats cleared |
| `device_events.exempted` | Device exempted |
| `device_events.uninstall` | Device uninstalled |

### 3.2 Product-Specific Device Events

#### Kiosk / MD Drive / MD CORE / MD ICAP

| Event Class ID | Description |
| ---- | ---- |
| `device_events.enrolled` | Enrolled |
| `device_events.deleted_by_admin` | Removed by an administrator |
| `device_events.unenrolled` | Unenrolled |

#### 3.3 Account Events

| Event Class ID | Description |
| ---- | ---- |
| `account_events.config_change` | Admin made configuration change |
| `account_events.logged_on` | Admin logged on |
| `account_events.logged_off` | Admin logged off |
| `account_events.failed_auth` | Failed login attempt |
| `account_events.user_created` | User created |
| `account_events.user_deleted` | User deleted |
| `account_events.password_reset` | Admin reset password |
| `account_events.account_privilege_modified` | Account privilege modified |
| `account_events.account_out_of_license` | License limit reached |
| `account_events.certificate_expiration` | Certificate nearing expiration |

## 4. CEF Extension Fields

#### 4.1 Device Event Extensions

| Key | Description |
| ---- | ---- |
| cs1Label | Custom field label (e.g. `deviceId`) |
| cs1 | Device ID value (MD Endpoint) |
| cs2Label | Custom field label (e.g. `deviceName`) |
| cs2 | Device name value (MD Endpoint) |
| dvchost | CM10 hostname |
| msg | Detailed event message |

#### 4.2 Account Event Extensions

| Key | Description |
| ---- | ---- |
| suser | Account email |
| dvchost | CM10 Hostname |
| msg | Detailed event message |

## 5. Examples

#### 5.1 Device Event

```javascript
CEF:0|OPSWAT|MOCM|10.3.2602|device_events.added|Device Added|2|
cs1Label=deviceId cs1=WinPer-id1768379914 \
cs2Label=deviceName cs2=WinPer-04-1768379914 \
dvchost=SonNgo \
msg=MetaDefender Endpoint (Version 7.6.2412.612) installed
```

#### 5.2 Account Event

```javascript
CEF:0|OPSWAT|MOCM|10.3.2602|account_events.account_privilege_modified|Account Privilege Modified|2|
suser=ocm@opswat.com \
dvchost=SonNgo \
msg=Administrator ocm (ocm@opswat.com) updated the co-admin son.ngo@opswat.com with Son role
```

> **Info**
>
> For further details about CEF see [https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/pdfdoc/cef-implementation-standard/cef-implementation-standard.pdf](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/pdfdoc/cef-implementation-standard/cef-implementation-standard.pdf).
