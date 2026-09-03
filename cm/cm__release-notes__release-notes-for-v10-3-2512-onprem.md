<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-3-2512-onprem -->

# Release Notes for v10.3.2512

### Release Date: Dec 26, 2025

Version: v10.3.2512

### **Release Highlights**

#### **Peripheral Media Protection Solution**

- Enhanced status and messaging for policy inheritance and version compatibility

Improved clarity in status indicators and system messages to better reflect policy inheritance rules and version compatibility, reducing confusion during configuration.

![](https://uploads.developerhub.io/prod/97qW/9wcokfc3r8rxi45yog69rk10hbm7hl1c1u823fl6nfibgadzpcgotzrw891z907c.png)

- Resolved inconsistencies between All Devices and the Kiosk tab

Fixed discrepancies in displayed information across the **All Devices** view and **Kiosk** tabs, ensuring consistent and accurate device data.

- Fixed performance degradation when viewing enrolled devices

Optimized backend processes to eliminate slow loading times when accessing large lists of enrolled devices.

- Block File Info in Export Reports

Added an option to include or exclude block file details in exported reports for improved customization and data privacy.

![](https://uploads.developerhub.io/prod/97qW/ti9a8jcsc8wecj31eq21r60qa77v1kzgtoqplx67t4wlecqvxbmator0shpvmwjg.png)

#### **Endpoint Security Solution**

- Added support to display scanning status in Device Detail

Device Detail pages now show real-time scanning activity, providing better visibility into ongoing security operations.

![](https://uploads.developerhub.io/prod/97qW/85ckc36xi7dihwftsyghhhmn1bl5czmpe6g49vvupv5q4ipgbckjpu9n2lyq07vl.png)

- Application patch upload

Added support for uploading application patches directly to My OPSWAT Central Management for streamlined patch management.

![](https://uploads.developerhub.io/prod/97qW/4ye76xjwrvqrjyqpjl44nbo7p28wi6v3z4pv0avgm4oinhg5g83ociyn9fc3opz8.png)

- Version-specific application patching

Introduced the ability to patch applications to a specific version, giving administrators greater control over update processes.

![](https://uploads.developerhub.io/prod/97qW/idyp5ft6l06n3bmvir10926g008xraasoc9kn9r6y1rnwtugaj01f0ur1bkn388i.png)

**File Security Solution**

- Reduce disk usage by skipping allowed files

Added an option to avoid storing allowed files, helping reduce disk space usage and optimize system performance.

![](https://uploads.developerhub.io/prod/97qW/kkr9dlh285in9kzflkjoizzp3ie2w5zhp6qwiswas9n3lkeiereyjr9evmper912.png)

- New Verdicts for Filtering

Added support for new verdicts in filtering, enabling more granular control and enhanced security policies.

*Notes: It's applicable from Core 5.17.0*

![](https://uploads.developerhub.io/prod/97qW/8ucn6cf5onezm02tuhz55lz0qfu7wlciw290w4387gdyfmyvyp2eh7dteti5lfn2.png)

- Added support to configure syslog events for ICAP

Administrators can now set up syslog event forwarding for ICAP-related activities, improving integration with SIEM and centralized logging systems.

![](https://uploads.developerhub.io/prod/97qW/p27ixuyh88dir7z1t4zntt9h9own5mb8z3oqloiqymsiqn8tx4467lbq18q8b8uj.png)

- Enhanced status and messaging for policy inheritance and version compatibility

Improved clarity in status indicators and system messages to better reflect policy inheritance rules and version compatibility, reducing confusion during configuration.

![](https://uploads.developerhub.io/prod/97qW/06ea36ioj4g7kpszxi31p40iiofuv2qx9xymk720sp510cep51i1g28g653r4uk9.png)

#### **Secure Access Solution**

- Added the ability to export protected applications

Administrators can now export a list of protected applications for reporting, auditing, or backup purposes.

![](https://uploads.developerhub.io/prod/97qW/zn43lksm348fbghfnc9p72oaa87u465uxuivuwds778xdp973sjwjo78vb1tknrz.png)

#### **Network Access Control Solution**

- Access Reject Default Access Profile

An Access Profile configured to reject authentication requests is now automatically added to the Default rule during initial system setup.

![](https://uploads.developerhub.io/prod/97qW/5lhotatb251dnt8np13vdllmq4mwj55agba94fc4rt2bmc0f8agf666a26bsi96h.png)

This profile can be applied to other rules as needed.

![](https://uploads.developerhub.io/prod/97qW/8vug2uikyz89181ld0oecimuaoowafzgxp0xat502er85yc1qruhxznwtkhvqnft.png)

- Internal bug fixed and improvements
