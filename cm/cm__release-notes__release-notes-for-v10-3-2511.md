<!-- source: https://www.opswat.com/docs/cm/release-notes/release-notes-for-v10-3-2511 -->

# Release Notes for v10.3.2511

### Release Date: Nov 20, 2025

Version: v10.3.2511

### **Release Highlights**

#### **Peripheral Media Protection Solution**

- Added support to display blocked files in Kiosk Details.

Administrators can now view a detailed list of files that were blocked during scanning sessions directly within the Kiosk Details page, improving visibility and troubleshooting.

![](https://uploads.developerhub.io/prod/97qW/0hrv81vhu6aaxqp3349khr2wyk1udquczr2098o50yqe24y09jpel95qusjyat5f.png)

- Improved PDF session scan reports for MetaDefender Kiosk & Drive.

PDF reports now include enhanced formatting and additional metadata, making it easier to review scan results and maintain compliance documentation.

- Added support for notifications when certificates are nearing expiration.

The system will proactively alert administrators when SSL/TLS certificates are close to expiring, helping prevent service interruptions and security risks.

![](https://uploads.developerhub.io/prod/97qW/8xhq9lfr4y6p3fsxcafqvtyhw9s1v7zteubz6rop5o3yv0vcv0grxoye3urzq9mi.png)

- Added support to view Kiosk license information.

License details for MetaDefender Kiosk are now accessible from the Inventory page, enabling quick verification of license status and expiration dates.

![](https://uploads.developerhub.io/prod/97qW/vckrqyckrmlj6tu33pordfjfu3svgkeo8mb08p6xaecj31rty0niowph731va10m.png)

- Fixed missing audit information

Added an audit log entry whenever an administrator updates Kiosk configuration settings, ensuring better traceability and compliance.

![](https://uploads.developerhub.io/prod/97qW/zju7qc2hyv9lxp817aect89u1mz2qoqv6cb0cvbod64l09i3tutqvo7hq57cq0xj.png)

#### **Endpoint Security Solution**

- Added support for required anti-malware applications on Android devices.

Administrators can enforce policies requiring specific anti-malware apps on Android endpoints, ensuring consistent security posture across mobile devices.

![](https://uploads.developerhub.io/prod/97qW/4rdur402f4wnc0gvyua5nkmv8xgag8e53zxkxoaj0amclap88tio0c3ld8jvp5fl.png)

- Introduced Malware Scan Detection Summary widget on the Dashboard.

A new widget under the Endpoint Security dashboard provides a quick overview of malware detection trends, helping security teams monitor threats and respond faster.

![](https://uploads.developerhub.io/prod/97qW/oyl1t8ke1lzguw2t313o2z4dsqkeclslauyj81j9vxowzzlb9syirfzjup5go40b.png)

#### **File Security Solution**

- Added support to display connection status, license status, and health status for MetaDefender Sandbox.

The management console now shows real-time operational and licensing information for Sandbox instances, improving monitoring and maintenance.

![](https://uploads.developerhub.io/prod/97qW/r4w09oepky7puww97qzlrbvt03ef6k9ug7ho2lax4lrezea9f868cc5r76mgs88t.png)

- Improved processing history export functionality.

Administrators can now export scan history reports exceeding 50,000 records. For large datasets, the export process runs in the background to avoid performance impact. Once completed, the exported file will be available for download under "Logs \ Export Events".

![](https://uploads.developerhub.io/prod/97qW/e204xp1a4hc3m34ldfabylont1oopd15uq0t361sokgwss9wy84qtawviqoabygk.png)

- Enhanced Overview Dashboard for MetaDefender Core.

The dashboard has been redesigned to provide clearer insights into system performance, scan statistics, and threat detection metrics.

![](https://uploads.developerhub.io/prod/97qW/ba2bhcv1gsj0apqzka47l87rzh2hab221pkwyrlzeq6r8o8jmcfuemlhwtfrly5b.png)

- Added support for license management for MetaDefender Sandbox and Managed File Transfer.

Administrators can now manage licenses for these products directly from the central console, streamlining license operations.

![](https://uploads.developerhub.io/prod/97qW/k6dts0a5gmkzafng4umb2qi72d2hidwci7d7fw1drety1e9wjlhoep1242clg66u.png)

- Added support to view Core license information.

License details for MetaDefender Core are now available in the Inventory for quick access and compliance checks.

![](https://uploads.developerhub.io/prod/97qW/8k7indf5n1oqua6o4xhyru7pu2mgjmge3sehrc1prw4l50l6xftm4ix4q4jnq45e.png)

#### **Network Access Control Solution**

- Fixed issue with IDP mapping for special characters.

Resolved a bug where identity provider mappings failed when usernames or attributes contained special characters.

#### **Additional Features**

- Enhanced Inventory filters for product type, connection status, and license status.

Inventory management now supports advanced filtering options, making it easier to locate and manage specific assets.

![](https://uploads.developerhub.io/prod/97qW/5dx7zluds55inlc7xc4n7awfn4fkm59dps2lir0tw17sejjbnl1p64d7df7uhv54.png)

- Added support for MetaDefender Managed File Transfer servers in Global Settings.

Administrators can configure and manage MFT servers globally, simplifying deployment and policy enforcement.

![](https://uploads.developerhub.io/prod/97qW/1a6djqgydspocmixjoywj74ls5j73vhb22n1wp257kgjz5esj32m52u2mbw86mks.png)

- Added support to sort by product version and local IP.

Sorting capabilities have been expanded to include product version and local IP address, improving usability when managing large environments.

![](https://uploads.developerhub.io/prod/97qW/cxm7glayrw6j480fxysxdaj77fxkzlatb0dr52rzyl2d36sh3t2ywmi6xgjwhrkv.png)
