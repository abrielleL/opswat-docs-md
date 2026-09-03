<!-- source: https://www.opswat.com/docs/cm/product-management/peripheral-media-protection -->

# Peripheral Media Protection

Peripheral Media Protection Dashboard gives you a centralized view of every piece of removable media entering your environment, and the health of the devices inspecting it. Use dashboard widgets to see what was blocked, understand why, and confirm your protection is actually running.

![](https://uploads.developerhub.io/prod/97qW/jhx0n7ss6w6di5wjlgfo07kee0k0xorcgmrocfvd9qzlstlhbogwzctm6v8mxl76.png)

## **Open Peripheral Media Protection Dashboard**

1. In the left navigation, select **Peripheral Media Protection > Dashboard**.
2. Choose the tab you need:
   1. **Security**: View the overall security status of peripheral media activity across your environment
   2. **Health**: Monitor product instance connection and health status

![](https://uploads.developerhub.io/prod/97qW/z40loizz0epoowqyjyhvp1wrb628jtdc541rmt5lz9h03oa0ulm1dsh7jq9v440z.png)

Use Filter by Group and Timeframe to scope the view. Widen the timeframe before concluding a widget is empty.

![](https://uploads.developerhub.io/prod/97qW/hrpw1qsw55ir60vae065tek23q93anr5zy5mvfrz0zkxkqdvs0fge73qpue2qsqx.png)

## Detect and Investigate Threats

The** Security **tab on the Peripheral Media Protection dashboard provides** interactive widgets** to help you detect and investigate file-based threats, data loss events, content sanitization outcomes, and USB device threats detected across your environment.

Quick jump to your specific focus:

1. [Assess overall media activity](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection#assess-overall-media-activity)
2. [Identify threat categories](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection#identify-threat-categories)
3. [Identify high-risk users and media types](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection#identify-high-risk-users-and-media-types)
4. [Investigate individual security incidents](https://www.opswat.com/docs/cm/product-management/peripheral-media-protection#investigate-individual-security-incidents)

### Assess overall media activity

Identify which security layer is driving the most interventions, so you can prioritize policy tuning and resource allocation.

| Widgets | What It Shows |
| ---- | ---- |
| Media Processing Sessions ![](https://uploads.developerhub.io/prod/97qW/k0815p22ayswggge5lfhub9npagi050kajl61cuzd0t7noja5utuatgedxrxq56m.png) | Shows the total number of media sessions within the selected timeframe, split into Allowed Media and Blocked Media |
| Blocked Media Breakdown ![](https://uploads.developerhub.io/prod/97qW/c3wf6jxklikrdjodg9dc02sdicngm98totbo1tyub1v9s01xkxpm2gmq8pp5cvzp.png) | Breaks down blocked sessions by the reason they were blocked |

### Identify threat categories

Five widgets drills down into the specific threat categories across all processed sessions

| Widgets | What It Shows |
| ---- | ---- |
| AI Threats Detected ![](https://uploads.developerhub.io/prod/97qW/2d88mhvircrcw34aokxk12gt1gqdodg30zkv7pckkrycwsg9g661d402eroyk00s.png) | Displays the total number of files flagged by the AI engine, with a breakdown visualizes the relative volume of each category |
| Threats Detected ![](https://uploads.developerhub.io/prod/97qW/8j007bohtv2cjk4cs9vz88fz7ql3dzqiuudc2b6192fumb671umd1x1xqy39y4o5.png) | Files identified as threats by traditional engines |
| Data Loss Prevented ![](https://uploads.developerhub.io/prod/97qW/c67h54j79l5jokwsap71vxyw8mi4g2b06d1n3gkgo7shoqqurhzlbd50dhy2a9to.png) | Files containing sensitive data categories that triggered a DLP rule  |
| Threats Prevented ![](https://uploads.developerhub.io/prod/97qW/2tkybvw32522ab7sbcy6t71e97qrlto09zta719latxepqlrtadx5s26h2ke16ej.png) | Files where content was sanitized (Deep CDR) to remove embedded threats before allowing access |
| Media Device Threats Detected ![](https://uploads.developerhub.io/prod/97qW/7w3cz09xit02sa4v32btdbhm7lefb5zl10q5vw1f3fn8nq5q2xe9snta3jy5b1xb.png) | Peripheral devices flagged by USB-threat detection (physical attack, deceptive device, unapproved device). Refer to [BadUSB Protection](https://www.opswat.com/docs/cm/product-management/badusb-protection) guidelines for more details |

### Identify high-risk users and media types

| Widgets | What It Shows |
| ---- | ---- |
| Blocked Sessions by Media Type ![](https://uploads.developerhub.io/prod/97qW/cbm4b1puvq86nrtf5iqa25gd07rvaecugkpr9eiaj2ix8mui5m3zn1d9l5jyzm7n.png)     | Shows how blocked sessions distribute across physical media types |
| Blocked Sessions by User ![](https://uploads.developerhub.io/prod/97qW/sce1tvao9wlvmxqi1vvs5wukxnv85215q2tz3qgeup81a5qotkv871svaegrc4jo.png) | Shows which users triggered blocked sessions. Users are identified by their authenticated identity at the Kiosk or Endpoint |

### Investigate individual security incidents

| Widgets | What It Shows |
| ---- | ---- |
| Blocked Media Sessions ![](https://uploads.developerhub.io/prod/97qW/pp1ac2jc07cdldifgn6d5kc2q20pgdvkustgvd92sqj2u61hpwnlwdwz6co52le4.png) - Select **Review** to open the full report, or **View Reports** for the complete list | Lists the most recent blocked media sessions in chronological order |

## Monitor Product Instance Health

The Health tab provides a real-time overview of your managed product instances. Use these widgets to quickly verify that your deployed instances are actively communicating with My OPSWAT Central Management and running supported software versions.

| Widgets | What It Shows | How To Interpret |
| ---- | ---- | ---- |
| Last Seen  | Shows when each device last reported to  My OPSWAT Central Management ![](https://uploads.developerhub.io/prod/97qW/zb6iw1qtie5tvirfxb35v0zjxo8phg6h3k2dwbs1vbjo329geenmrqj98gs9fp88.png) | - A healthy deployment should show the majority of devices in the **Within 1h** or** 1–24h ago** segments - If a significant portion of devices appear in the **> 30d ago** segment, verify network connectivity, confirm the agent service is running on those devices, or determine if those instances have been retired |
| Version Status | Indicates whether each device is running the latest supported software version ![](https://uploads.developerhub.io/prod/97qW/3wd2i7bypr4m27ku7f9e51evd25us76t2bj8b3dbs7l18f0hcgfhrbi0y2xboo2m.png) | - Aim for all devices to show **Up To Date**. Out-of-date instances may lack critical security patches or feature improvements - Use the [Update Application](https://www.opswat.com/docs/cm/product-management/update-application) feature to push updates to out-of-date devices |
