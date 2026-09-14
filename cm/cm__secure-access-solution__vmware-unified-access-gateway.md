<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/vmware-unified-access-gateway -->

# Omnissa Unified Access Gateway

My OPSWAT Central Management can be enhanced by using Omnissa Unified Access Gateway (UAG) to check device compliance before letting a user access to a VDI. [Learn more about this integration](https://www.opswat.com/partners/vmware).

By integrating My OPSWAT Central Management into Omnissa Unified Access Gateway solutions, administrators are able to check remote devices for:

- **Vulnerabilities -** Detect vulnerabilities on endpoints through installed applications and operating systems.
- **Enhanced Compliance** - Get greater visibility into the status of installed security applications such as hard disk encryption and system information, or such as password protection, to ensure devices are compliant with existing policies.
- **Unwanted Applications** - Detect and remove non-compliant or unwanted applications such as peer-to-peer applications from a remote device.
- **Advanced Threat Detection** - Utilizing two methods of advanced threat detection, My OPSWAT Central Management helps identify potential threats that existing anti-malware software might not protect against.
- **Portable media scanning and access control** - Protect organizations against threats from portable media on the endpoints, a common attack vector for malware.
- **Anti-screen capture** - Prevent keyloggers and advanced malware from accessing sensitive data.
- **Screen capture protection** - Prevent unauthorized or accidental screenshots and recording by users, VDI, web collaboration tools, and malicious applications.

Documents:

- [How to set up Omnissa Unified Access Gateway with On-Demand MetaDefender Endpoint](https://www.opswat.com/docs/cm/secure-access-solution/how-to-set-up-omnissa-unified-access-gateway-with-on-demand-meta)
- [Troubleshooting guideline](https://docs.vmware.com/en/Unified-Access-Gateway/3.1/com.vmware.uag-31-deploy-config.doc/GUID-988086FD-CD52-455A-A934-C219C9DAC2CC.html)

You can set up a My OPSWAT Central Management account to manage up to 50 devices with free of charge. [Start Trial Now](https://gears.opswat.com)

## Frequently Asked Questions

### 1. Why does a user can access VDIs even their device is non-compliance through web access?

The Horizon Endpoint Compliance feature with OPSWAT My OPSWAT Central Managementis currently supported for Omnissa native Horizon clients. With HTML Access, no policy check is made. However, you can turn on or off the disable HTML access setting on Omnissa UAG to either fully deny or allow access.

To deny all HTML access, you can follow the below steps:

- Log into Omnissa UAG console admin
- Open Edge Service Settings > Horizon Settings

![](https://uploads.developerhub.io/prod/97qW/dudei1g0qzsiv61x9142jl39lus09t5j8jo1fe8dnbdffp14ctckeww6u83mcqlc.png)

- Turn on "Disable HTML Access" setting

![](https://uploads.developerhub.io/prod/97qW/w5odcs0ol67b90hile39whs78vsl9xwadgtceitb6em9popllkjbhcqfpu6j6hrj.png)

- Click SAVE

### 2. Does this integration support Android users?

This integration may work on some Android devices if the Omnissa Horizon app and OPSWAT Mobile app can retrieve a device's MAC address. This requires the device to install OPSWAT Mobile app and be enrolled it to the My OPSWAT Central Management account.

### 3. Does this integration support iOS users?

From Omnissa UAG version 3.8+, it now supports iOS users. The user experience will be different compared with the user experience on PCs.

### 4. What domains and IP addresses should I allowlist on my firewall/proxy?

If your devices or your UAG sits behind a firewall or a proxy, you need to allowlist domains to allow UAG and devices talk to OPSWAT My OPSWAT Central Management. See more details at [How do I configure MetaDefender Endpoint to work with a proxy or outbound firewall?](https://www.opswat.com/docs/macloud-sdp/3.54.0/kb/how-do-i-configure-opswat-client-to-work-with-a-proxy-or-outboun)

You need to configure UAG outbound connection to Internet which is on the Internet facing NIC to able to contact the OPSWAT My OPSWAT Central Management servers, please refer Omnissa[ documents](https://communities.vmware.com/docs/DOC-32926) for more details. Please note that the domain *gears.opswat.com* is not assigned static IP addresses. If you need static IP addresses to configure on UAG/firewall, we have domain *dapi.opswat.com* as an alternative domain for gears.opswat.com and it's assigned static IP addresses.

### 5. Where can I find On-Demand MetaDefender Endpoint's log when it's triggered from Horizon Client?

You can find On-Demand MetaDefender Endpoint's log at:

- Windows
  - C:\Users<username>\AppData\Local\Omnissa\Omnissa Horizon Client\Code Cache<uuid>\ while Horizon Client session is still on.

![](https://uploads.developerhub.io/prod/97qW/9j490x6x10bvaqes71qcmehtaisrs96p6ev84bp1y036v68suydzt0zitk7zrlxo.png)

- For Omnissa Horizon Client log :C:\Users<username>\AppData\Local\Omnissa\Horizon\logs

![](https://uploads.developerhub.io/prod/97qW/313gvceo0o1gtdu6bllup92fhkqczdi1zlhuu0o4eic6knb3bizhohaw7t6rs9m7.png)

- macOS
  - /Users/<User name>/Library/Logs/Gears/logs/<License Key>/GEARS-Ondemand.log

![](https://uploads.developerhub.io/prod/97qW/068x7zkk4e23w5tppg49kptekpreiaqhbv0hy7wu626agkxkjil5f38diw5xftjj.png)

- For Omnissa Horizon Client log: /Users/<username>/Library/Logs/Omnissa Horizon Client/

![](https://uploads.developerhub.io/prod/97qW/2hhr5bxqdaq9czxilys5h6r1xhir6bcnfb6f90uvtard0pejwmura2ixofgg7sow.png)

6. Why couldn't Horizon Client distribute On-Demand MetaDefender Endpoint on devices?

The minimum version of Horizon Client that supports this feature is 5.4 and make sure you upload an on-demand client to Unified Access Gateway v3.9+.

- If a user runs an older version, please upgrade Horizon Client to a version 5.4.
- If a user already run Horizon Client 5.4.x, please contact Omnissa support to troubleshoot the issue.

To restrict minimum Horizon Client running on a device, you can refer [this guideline](https://docs.vmware.com/en/VMware-Horizon-7/7.13/horizon-console-administration/GUID-4842881A-1D1B-432F-8CA2-37FA9A1E2EB9.html) on Omnissa.

### 7. Why couldn't Horizon Client distribute On-Demand MetaDefender Endpoint on macOS devices?

This is a known issue if you are running Horizon Client version 5.4.x and previous versions and your administrators do not add any parameters into CLI on UAG. As a workaround solution, you should add parameters to the CLI on UAG, such as /log 1 as the below screenshot to fix it.

For more information about parameters available on On-Demand MetaDefender Endpoint, you can visit [On-demand Client CLI](https://www.opswat.com/docs/cm/configurations/on-demand-client-cli).

### 8. How to know On-Demand MetaDefender Endpoint has been downloaded by Horizon Client?

**First step:** Please check the settings:

- Client Key and Client Secret
- Hostname
- Path To Executable
  - For macOS: Please follow format: OPSWAT_GEARS_Client_<very_long_filename>.app/Contents/Resources/opswat-gears-od
  - Example: OPSWAT_GEARS_Client_3445-a44 ***ba.app/Contents/Resources/opswat-gears-od

**The second step:** Check Horizon Client has successfully downloaded OPSWAT On-Demand MetaDefender Endpoint

***For macOS:***

- Check the folder: /Users/<Username>/Library/Application Support/Omnissa Horizon Client/Code Cache/<uuid> there is a .zip file
- Check the .zip file to see the correct information such as server name, license key, agent version

![](https://uploads.developerhub.io/prod/97qW/kojg6j06hr96vec9gqpf4go4dj2bbn5dwkzrmn1mvvvdnf9s0ukwmyqtlspl2rnd.png)

If failed: check in Endpoint Compliance Check Provider Settings and re-upload agent correctly

***For Windows:*** check the On Demand file to see the correct information such as server name, license key, agent version

Please check:

- C:<username>\AppData\Local\Omnissa\Omnissa Horizon Client\Code Cache<uuid>

![](https://uploads.developerhub.io/prod/97qW/hvift5o0ystq9aldr31juvw0wjxo71huz6s9yp5t7pacefjb3brakguvazptde3z.png)

### 9. How to check Horizon Client start with On-Demand MetaDefender Endpoint?

**For macOS:**

Check in Activity Monitor for process opswat-gears-od when connecting to Horizon Client

![](https://uploads.developerhub.io/prod/97qW/iefs8p4zt0bbj901qdhoxipfko5ahzrfqt9f8faqj945zo4gpzb4giy9yr0ydn8x.jpg)

If failed:

- Add execute permission chmod +x opswat-gears-od
- Try run opswat-gears-od
- Check Path To Executable on Endpoint Compliance Check Provider Settings (UAG setting)

**For Windows:**

Check at Task manager for process OnDemand when connecting to Horizon Client

![](https://uploads.developerhub.io/prod/97qW/ze3et0bjv4r76ykckqnul9a9ssqjgvdloc0svdp8bwjn5dr8g762bqfskdaob47y.jpg)

If failed:

- Try run opswat-gears-od
- Check Path To Executable on Endpoint Compliance Check Provider Settings (UAG setting)
