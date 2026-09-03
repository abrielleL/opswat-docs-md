<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-generate-a-support-package-for-my-opswat-central-manageme -->

# How to generate a support package for My OPSWAT Central Management?

> **Check Your Product:**
>
> This article is relevant for My OPSWAT Central Management (on-premises) on Windows systems starting from version 10.0.2506 and later, or on Linux systems from version 10.2.2509.

A support package is a collection of log and configuration files which are used by the OPSWAT Support team when troubleshooting My OPSWAT Central Management Issues.

A support package can be generated in either Windows or Linux systems, by following the relevant instructions below.

## Windows

You can generate the support package directly from the tray menu:

![](https://uploads.developerhub.io/prod/97qW/18b2c5st7vr47suy4qoctuct15ddxe66njsm1cow3thvcjco3b7m65qtelmbscrg.png)

### Additional options to generate the support package

1. Navigate to the **My OPSWAT Central Management installation directory** (default path: `C:\Program Files\OPSWAT\MOCM`).

![](https://uploads.developerhub.io/prod/97qW/y9sui2rrfotziynvjot7xm0cl6maqcz45sdpor0acz8ine8x4y3akb26250xjpf8.png)

2. Right-click `mocmSupportPackage.exe` and choose “Run as administrator,” or simply double-click it and approve the UAC prompt if it appears. You can also run it from an elevated Command Prompt.

![](https://uploads.developerhub.io/prod/97qW/lozaqtem9ysd0ksttrogvkzqshq3wbfwcuw8ccuiq9przrwbrz85gxjpanvug3xk.png)

![](https://uploads.developerhub.io/prod/97qW/hhzx8rtcw2s1yargb2s1you9zjg6xt6ddfr5sh2wg2d76npxexo38ktg3egndtkq.png)

3. The package will be generated in the format of **mocm-support-package-<timestamp>.zip**, inside the installation folder, to be copied and forwarded to **OPSWAT Support**.

![](https://uploads.developerhub.io/prod/97qW/ns1ud1imy3f27xyxh9skvwanljhhkau4hkb667z1v2xxw6lgwt9itzza69wr8l0q.png)

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
