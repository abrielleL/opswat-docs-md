<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-should-i-do-if-one-or-more-devices-could-not-resolve-cross- -->

# What should I do if one or more devices could not resolve cross-domain API URL?

> **Check Your Product:**
>
> This article applies to the current Cross-Domain API and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

Cross-Domain API is a mechanism that allows 3rd party solutions to interact with the MetaDefender Endpoint to retrieve the device IDs of devices on which the MetaDefender Endpoint is installed. To learn more, see [Cross-domain API](https://www.opswat.com/docs/cm/developer-guidelines/cross-domain-api).

MetaDefender Endpoint uses the **eapi.opswatgears.com** domain for this API, and it should be resolved to a loopback IP address such as, for example, **127.0.0.1**.

Should you try to resolve the **eapi.opswatgears.com** domain from a configured DNS server on your device, only to get a **No/Incorrect** result, please contact your administrators to troubleshoot the issue.

While you wait for a permanent solution from your administrators, you can add that domain to a hosts file on your device as a temporary workaround, by following the steps below.

## On Windows devices

1. Open the Windows **Start** menu, search for **Notepad**, then choose **Run as administrator**, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/ltygf8z8z7ug5if0zzufjeytmjrxoi7jixgle088kpo3h3h8w7tkc6dypb2d6zh9.png)

2. In notepad, choose to **File>Open**

![](https://uploads.developerhub.io/prod/1yda/iv46dyj0yz03je8ukvw29q3ajm240zrszjussx61iinbl1fu5n6aqzihqacufxdz.png)

3. Now, into the **File name** field, as illustrated below, paste **C:Windows\System32\drivers\etc\hosts.tx**t, then click **Open**.

![](https://uploads.developerhub.io/prod/1yda/ox3g7n2uv4xcs6xoj9ldzgsfcst6z76skcu1oqpkpu0p7nqskwm2s42at22okn5a.png)

4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the bottom of the text, as illustrated below, then click **File>Save**.

![](https://uploads.developerhub.io/prod/1yda/ggmeval4dnp2hkocxm68xedk8jtsshdrlzzl73kqux1t8u6gwqorpcdkgobdbt6l.png)

## On macOS devices

1. Launch a **Terminal**.
2. In the command line, type **sudo nano /etc/hosts**, then hit **Enter**.

![](https://uploads.developerhub.io/prod/1yda/y780ldzi75caixepw4epu18vus79h6d639ygd41fqo81lzukn6ounyjtohy75lup.png)

3. Enter your admin **Password** as prompted, then hit **Enter** again.
4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the text, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/nz756yzn6p9z8wqd3h6suzo1lp16smw8fplpbpwe15a7hbjnm4uwz1znjn6q8a5m.png)

5. Once added, hit **Ctrl O**, followed by **Enter** to save your changes, then hit **Ctrl X** to exit the nano editor.

## On Linux devices

> **Please Note:**
>
> The following steps were recorded in Ubuntu, but interfaces may vary per distro.

1. Launch a **Terminal**.
2. Type **sudo nano /etc/hosts** and then hit **Enter**.

![](https://uploads.developerhub.io/prod/1yda/x3moe0iyd0g6xedag9pgnz3amzkzqpwmjkkt81sehlsnm7tdijhtltj5mkdn1g7s.png)

3. Enter your admin **Password**, as prompted.
4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the top of the text, as illustrated below.

![](https://uploads.developerhub.io/prod/1yda/jq26fpi3weo10ly8wxnx6a0ck81lx3sp3vuupip30gq40q080hcq6m8gqtk6tt88.png)

5. Once you’ve edited the text, hit **Ctrl X** and then **Y** to save your changes.

> **Support:**
>
> If you have applied this temporary solution but your administrator Is **Unable To Find A Permanent Solution To One Or More Devices Being Unable to Resolve The Cross-Domain API URL**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
