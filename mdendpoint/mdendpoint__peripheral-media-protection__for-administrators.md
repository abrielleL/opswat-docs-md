<!-- source: https://www.opswat.com/docs/mdendpoint/peripheral-media-protection/for-administrators -->

# For administrators

To configure and set policies for Peripheral Media Protection and Peripheral Device Control features on managed endpoints running MetaDefender Endpoint, please follow the detailed guideline as below

## Navigation

**Step 1:** Login to the management console in My OPSWAT Central Management

**Step 2:**

- For Peripheral Media Protection configuration: *Peripheral Media Protection > Policies > Peripheral Media Protection*
- For Peripheral Device Control configuration: *Peripheral Media Protection > Policies > Peripheral Device Control*

![](https://uploads.developerhub.io/prod/2x2P/4bftnynr18h6y0x27enrei9ntcbwb0o0ti95i3vb20w6d0evy2npfufzaes1xjij.png)

> **Note**
>
> Starting with **My OPSWAT Central Management version 10.7.26062** (released on June 30, 2026), the management console for Peripheral Media Protection and Advanced Endpoint Protection is revamped with a restructured left menu, simplifying navigation to key protection controls.
>
> With this revamp, no configuration is lost due to this interface changes. Your existing policies and settings will be carried over automatically.

> **Info**
>
> For customers using previous versions of My OPSWAT Central Management (before 10.7.26062), the management console will remain as is until upgrade.
>
> For more details about Before vs. After and what has been changed, please refer to this [Documentation](https://www.opswat.com/docs/cm/knowledge-base/Left-Menu-Revamped-v10-7-26062)
>
> For details on configuring Peripheral Media Protection policies for managed endpoints using previous My OPSWAT Central Management versions, please refer to this [User Guide](https://www.opswat.com/docs/mdendpoint/user-guide/peripheral-media-protection-feature)

As a result, this documentation provides details on configuration, policy set up, and monitoring for peripheral media usage and data transfers using **My OPSWAT Central Management version 10.7.26062 or later**

## Configuration

### Peripheral Media Protection

**Step 1:** Navigate to *Peripheral Media Protection > Policies > Peripheral Media Protection > Windows/macOS*

![](https://uploads.developerhub.io/prod/2x2P/4bftnynr18h6y0x27enrei9ntcbwb0o0ti95i3vb20w6d0evy2npfufzaes1xjij.png)

**Step 2:** Click on *Configuration* tab. This is where you can configure actions applied on connected peripheral media.

![](https://uploads.developerhub.io/prod/2x2P/fakq29c0pba1eobyo44dhqhmqx98nk2qwp0pi575wlpyjf0nt6a2ou5hmoeaih8j.png)

#### Exclude Device

Admins can configure to exclude specific type of removable media device from being blocked by MetaDefender Endpoint when inserted to the endpoint and exempt from scanning. Media type include:

- CD/DVD
- Mobile devices
- Unformatted media
- Virtual ISO Drives

#### Allowlist

- With this feature, administrators can allow removable media devices based on Device ID, Vendor ID or instance path
- Administrators can also grant time-limited, exception-based access to specific peripheral devices for authorized individual/endpoint based on policies

![](https://uploads.developerhub.io/prod/2x2P/l386hip6pfl0nhc11lx7rzd35tx4tpmen5p9fd7d8da9lnw7bmqv8bi81j2hgtek.png)

#### Peripheral Media Protection Modes

This feature has **three different modes** that are controlled and set via the administrator management console.

![](https://uploads.developerhub.io/prod/2x2P/o5nt4v6kf4z9enx33r0pnm8uzse6pffws0spesnvbdepfy5onkalkxj8dg0rjst4.png)

- **Always block:** Full block mode. Peripheral media devices will be fully blocked with this mode, and users need to scan the device to unblock.
- **On-access scanning:** To access files from peripheral devices, users can choose to scan selected files that they wish to work on or scan the entire USB. Users can select files directly from native apps like Windows Explorer to maintain a natural workflow
- **Allow selected actions:** Block the peripheral media device and allow users to take specific actions.

### Mode 1: Always block

Peripheral media devices will be fully blocked with this mode, and users need to scan the device to unblock.

![](https://uploads.developerhub.io/prod/2x2P/4wxexupc9u1du99l9dcbf9jzk0pzn02bfyonsud0qumr7czj5gnd3uwj5numgfit.png)

### Mode 2: On-access scanning

#### Configuration

Admins can configure settings for sanitized files with Content Disarm and Reconstruction (CDR) in this section

![](https://uploads.developerhub.io/prod/2x2P/ofqsimt6pjepcpk8uwziqnibzvqk1arjglf3rt78v1rria6dl4wkw79r5fvltvd3.png)

Admins can also **configure corresponding behaviors when a scan is finished or failed**

![](https://uploads.developerhub.io/prod/2x2P/ps02a129y2gcix6y3notnifplzbx7m4mmh0f1mnvhln31wcwjopewbic3xceo4n0.png)

**Configurable File Bypass**

Admins can configure to allow users to skip individual file scans or device blocks for immediate access in Peripheral Media Protection

![](https://uploads.developerhub.io/prod/2x2P/b5ye2u7hkl7nx31l7m013b7fxpm5zpvm6yppxljsbbg3eqt80nzvu25jdix7sa4f.png)

**Configure media manifest usage**

![](https://uploads.developerhub.io/prod/2x2P/9mz3o36ouvylwp99zjc72jquvetu2i70a8jncjsoonl493zzr36g3kupumnf3ngk.png)

Setting for peripheral media data transfer using Managed File Transfer (MFT). Admins can configure for users to upload allowed/blocked files to Managed File Transfer from removable media devices

![](https://uploads.developerhub.io/prod/2x2P/182k5lx8554h7mp09173qf4kzsu035o0rranpqtc76r84hkzvc8uzfuvwn2o5355.png)

#### Scan Workflow

Administrators can configure the scanning workflow for removable media device in this section

![](https://uploads.developerhub.io/prod/2x2P/vrlt8ueveo6o7qrk5aqqjw9z325xovowhbeu1p1g49rwdme54biishf81eeuxsbj.png)

> **Info**
>
> Scan workflow tab is only enabled for ***On-access scanning*** mode and ***Allow selected actions*** mode

![](https://uploads.developerhub.io/prod/2x2P/q05uo7dokkzsizznhpv2n7zcs2nmfedz98ruu260jm1vozdv4tgyilss98kwv8rx.png)

> **NOTE**
>
> This scan workflow applies to MetaDefender Endpoint agent version 7.6.2606.xxxx and later. Devices running older versions will use the scan workflow in Malware Scan under Endpoint Security policy tab.

Settings that administrators can configure include:

**Scanning server:** Add scan server and set relevant rules

![](https://uploads.developerhub.io/prod/2x2P/uf6h8ypho4ek4gzazfrkpc3sl7nakq614hkn9tjf35zibccgjw9ghu4i4x1juiwh.png)

![](https://uploads.developerhub.io/prod/2x2P/asi7srdjg8jd8fsp3q6h3ki8uy2s3s4aridj86yf48miyfmilvla0o7igtm3lbvu.png)

If multiple scanning servers are available, administrators can configure the server priority by specifying the order (for example, primary, secondary, and so on, simply by using the drag-and-drop icon on the left-hand side or the arrow buttons on the right-hand side

![](https://uploads.developerhub.io/prod/2x2P/rbzyc1ql2p5c4n09sy41lonvv9hdjqu8bux8366klisgd72da6lfh24rms9z3rmc.png)

**Automatic Scan Server Failover: **When the primary scanning server becomes unreachable, Peripheral Media Protection automatically fails over to another available scan server

**File exceptions**

![](https://uploads.developerhub.io/prod/2x2P/7p4gdq6d2wdi5070vecnvca4wik6pba2mkvn97jhfnukph13axjclqq3qhw1j42z.png)

**Threat detection modes, NTFS Alternative Data Stream Detection and Scanning performance**

![](https://uploads.developerhub.io/prod/2x2P/eev1cdqubqwkm0nabqpaiwijszbupib7yfr64gg01qo0q39u08wmzleqas9hgkfu.png)

### Mode 3: Allow selected actions

#### Configuration

Administrators can configure to allow users take specific actions on all or specific removable media (using ID Strings or Regular Expressions) when it is connected

![](https://uploads.developerhub.io/prod/2x2P/389m85abl8j3qv3tsv10luybbkuwo58nsip42v7y1ix02jz8hfxfwvvqyg5lwqvl.png)

Actions that can be taken:

- Unblock when no threat is found
- Copy to/from removable media devices
- Configurable option to only allow copy to/from approved folders

![](https://uploads.developerhub.io/prod/2x2P/mbyjjbjnlyy4faomaly37qlsukiz3i8toybajvph2wyxfr00mjcarx0px7y1439r.png)

Admins can configure designated locations to copy allowed and unvalidated files from removable media

![](https://uploads.developerhub.io/prod/2x2P/sdk6d80l7u3834ciemfisxhgo256b1iw5ace96sskefl47l5wqldmobcrlega268.png)

**Scanning reports: **

- Reports can be extracted in PDF or CSV formats
- Configure reports details

![](https://uploads.developerhub.io/prod/2x2P/ber4ktxkqmqbyyfj56jbgi2avmo0xf56hzt5t22t1swl6eml0d2l7obxa0sib38m.png)

Admins can configure settings for sanitized files with Content Disarm and Reconstruction (CDR) in this section

![](https://uploads.developerhub.io/prod/2x2P/zl2rsjfi5kqffomq83qxhzwwdost9yh8qekj8q7v4hi6ag3pynbra68698dhrdmj.png)

Configurable auto-scan

![](https://uploads.developerhub.io/prod/2x2P/oxm44cn3pxwjt1dea9p7rd2b5e4s16s146ugngycqyeqf9mzwrdlsc5gzmozs3m1.png)

Admins can also **configure corresponding behaviors when a scan is finished or failed**

![](https://uploads.developerhub.io/prod/2x2P/ps02a129y2gcix6y3notnifplzbx7m4mmh0f1mnvhln31wcwjopewbic3xceo4n0.png)

**Configurable File Bypass**

Admins can configure to allow users to skip individual file scans or device blocks for immediate access in Peripheral Media Protection

![](https://uploads.developerhub.io/prod/2x2P/b5ye2u7hkl7nx31l7m013b7fxpm5zpvm6yppxljsbbg3eqt80nzvu25jdix7sa4f.png)

**Configure media manifest usage**

![](https://uploads.developerhub.io/prod/2x2P/9mz3o36ouvylwp99zjc72jquvetu2i70a8jncjsoonl493zzr36g3kupumnf3ngk.png)

#### Scan Workflow

Administrators can configure the scanning workflow for removable media device in this section

![](https://uploads.developerhub.io/prod/2x2P/vrlt8ueveo6o7qrk5aqqjw9z325xovowhbeu1p1g49rwdme54biishf81eeuxsbj.png)

> **Info**
>
> Scan workflow tab is only enabled for ***On-access scanning*** mode and ***Allow selected actions*** mode

![](https://uploads.developerhub.io/prod/2x2P/q05uo7dokkzsizznhpv2n7zcs2nmfedz98ruu260jm1vozdv4tgyilss98kwv8rx.png)

> **NOTE**
>
> This scan workflow applies to MetaDefender Endpoint agent version 7.6.2606.xxxx and later. Devices running older versions will use the scan workflow in Malware Scan under Endpoint Security policy tab.

Settings that administrators can configure include:

**Scanning server:** Add scan server and set relevant rules

![](https://uploads.developerhub.io/prod/2x2P/uf6h8ypho4ek4gzazfrkpc3sl7nakq614hkn9tjf35zibccgjw9ghu4i4x1juiwh.png)

![](https://uploads.developerhub.io/prod/2x2P/asi7srdjg8jd8fsp3q6h3ki8uy2s3s4aridj86yf48miyfmilvla0o7igtm3lbvu.png)

If multiple scanning servers are available, administrators can configure the server priority by specifying the order (for example, primary, secondary, and so on, simply by using the drag-and-drop icon on the left-hand side or the arrow buttons on the right-hand side

![](https://uploads.developerhub.io/prod/2x2P/rbzyc1ql2p5c4n09sy41lonvv9hdjqu8bux8366klisgd72da6lfh24rms9z3rmc.png)

**Automatic Scan Server Failover: **When the primary scanning server becomes unreachable, Peripheral Media Protection automatically fails over to another available scan server

**File exceptions**

![](https://uploads.developerhub.io/prod/2x2P/7p4gdq6d2wdi5070vecnvca4wik6pba2mkvn97jhfnukph13axjclqq3qhw1j42z.png)

**Threat detection modes, NTFS Alternative Data Stream Detection and Scanning performance**

![](https://uploads.developerhub.io/prod/2x2P/eev1cdqubqwkm0nabqpaiwijszbupib7yfr64gg01qo0q39u08wmzleqas9hgkfu.png)
