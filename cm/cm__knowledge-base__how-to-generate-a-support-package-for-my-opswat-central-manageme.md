<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme -->

# How to generate a support package for My OPSWAT Central Management?

> **Check Your Product:**
>
> This article is relevant for My OPSWAT Central Management (on-premises) on Windows systems starting from version 10.0.2506 and later, or on Linux systems from version 10.2.2509.

A support package is a collection of log and configuration files which are used by the OPSWAT Support team when troubleshooting My OPSWAT Central Management Issues.

A support package can be generated in either Windows or Linux systems, by following the relevant instructions below.

## From the My OPSWAT Central Management console(from version 10.7.26080 and later)

The recommended way to generate a support package is from the web console, which works for both Windows and Linux deployments and does not require access to the server.

1. Log in to the My OPSWAT Central Management console with an administrator account.
2. Open the **Help Center** and select the **Support Packages** tab.

   ![](https://uploads.developerhub.io/prod/97qW/byqtx982m79ue9teopx2zgfezn8zlr5graljmttt6cbtm2tijwmlsstl212b4wjb.png)
3. Click **Generate Support Package** (top-right corner).
4. In the **Generate Support Package** dialog, select **My OPSWAT Central Management**.

   > **Note:** The same dialog can also be used to generate support packages for managed products, such as **MetaDefender Core** or **MetaDefender Kiosk Windows**.
5. Click **Generate Support Package** to start the generation.

![](https://uploads.developerhub.io/prod/97qW/g7m6e3edhrxib505hbx4r4rhc6uvpj0nwxc44yt7h1ktlbijwv543txgu9ksh4b3.png)

6. Once generation completes, the package is listed under the **Support Packages** tab. You can search for it by package name or filter by attribute, then download it and forward it to **OPSWAT Support**.

If the console is not accessible, use one of the server-side methods below.

## Windows

You can generate the support package directly from the tray menu:

![](https://uploads.developerhub.io/prod/97qW/dalr114u1unvaoalu81htl33yi7kvx81coj27da6hhpm7wzowfhnp8laq9x11cu4.png)

### Additional options to generate the support package

1. Navigate to the **My OPSWAT Central Management installation directory** (default path: `C:\Program Files\OPSWAT\MOCM`).

![](https://uploads.developerhub.io/prod/97qW/445b8oe5nuzm8ujc9pllnp1gs1xqqirk8f30bc72cuia08nxug6x0xoefroftluv.png)

2. Right-click `mocmSupportPackage.exe` and choose “Run as administrator,” or simply double-click it and approve the UAC prompt if it appears. You can also run it from an elevated Command Prompt.

![](https://uploads.developerhub.io/prod/97qW/kyw5fa7m1eruiynnkdlifntr1tdh8lmfll9j0kxbrto2w912dq87yqeys0d7zvsq.png)

![](https://uploads.developerhub.io/prod/97qW/jtinvujhssbx3hva03qyiiks2g0tgme7sh0f18oey1jdjr92y61bq12qbiydfgla.png)

3. The package will be generated in the format of **mocm-support-package-<timestamp>.zip**, inside the installation folder, to be copied and forwarded to **OPSWAT Support**.

![](https://uploads.developerhub.io/prod/97qW/ccnfx04mhiy6bmg3wydrben5jm90ojv9487i7kkt1yc6jszpp5os1gwr4xtic49y.png)

In cases where the support package generator is also unable to function properly, please follow the below instructions to manually collect the log files

1. Locate OPSWAT Central Management installation folder (default C:\Program Files\OPSWAT) and the System Drive (default C:)
2. Collect the following folders/files
   - <installation folder>\MOCM\nginx\conf
   - <installation folder>MOCM\nginx\logs
   - <installation folder>\MOCM\tomcat\logs
   - <System Drive>\ProgramData\OPSWAT\MOCM\Logs

## Linux - Red Hat Enterprise/Red Hat

1. Open a **Terminal** and navigate to **/opt/mocm/lib/**
2. Execute **generate-support-package.sh ,** with Root privileges or, if needed, grant execute permission via chmod.
3. The package will be generated in the format of **mocm-support-package-<timestamp>.tar.gz**, inside the **/opt/mocm/lib** folder.

In cases where the support package generator is also unable to function properly, please manually collect the following folders and files:

- /var/log/mocm folder
- /var/log/redis folder
- /var/log/rabbitmq folder
- /var/log/nginx folder
- /etc/redis folder
- /etc/rabbitmq folder
- /etc/nginx folder
- /opt/mocm/apps/conf all properties files .properties

```bash
find /opt/mocm/apps/conf -name '*.properties*'
```

- /opt/mocm/apps/ all log files .log

```bash
find /opt/mocm/apps/ -name '*.log*'
```

- /opt/mocm/apps/ all override files .override

```bash
find /opt/mocm/apps/ -name '*.override*'
```

> **Support:**
>
> After generating your package, please open a [**Support Case**](https://my.opswat.com/portal/support) with the OPSWAT team via the form method, uploading your My OCM logs as prompted.

> **Warning:**
>
> Depending on the total size of the My OPSWAT Central Management server's log files. it may take a long time for the support package generation process to complete.

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
