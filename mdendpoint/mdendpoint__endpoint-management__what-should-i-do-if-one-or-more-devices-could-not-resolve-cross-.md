<!-- source: https://www.opswat.com/docs/mdendpoint/endpoint-management/what-should-i-do-if-one-or-more-devices-could-not-resolve-cross- -->

# What should I do if one or more devices could not resolve cross-domain API URL?

> **Check Your Product:**
>
> This article applies to the current Cross-Domain API and all MetaDefender Endpoint releases deployed on Windows, macOS and Linux systems.

Cross-Domain API is a mechanism that allows 3rd party solutions to interact with the MetaDefender Endpoint to retrieve the device IDs of devices on which the MetaDefender Endpoint is installed. To learn more, [Read This](https://docs.opswat.com/macloud-sdp/developer-guide/cross-domain-api).

MetaDefender Endpoint uses the **eapi.opswatgears.com** domain for this API, and it should be resolved to a loopback IP address such as, for example, **127.0.0.1**.

Should you try to resolve the **eapi.opswatgears.com** domain from a configured DNS server on your device, only to get a **No/Incorrect** result, please contact your administrators to troubleshoot the issue.

While you wait for a permanent solution from your administrators, you can add that domain to a hosts file on your device as a temporary workaround, by following the steps below.

## On Windows devices

1. Open the Windows **Start** menu, search for **Notepad**, then choose **Run as administrator**, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/4xwi41r9ahvn4djsoq8t5m84bwh1f6zk99krc0vnif4j1mcmlva9k6avlmye7l6m.png)

2. In notepad, choose to **File>Open**

![](https://uploads.developerhub.io/prod/2x2P/b43im7ctw6sg3hqwj5s5gg8nyrf78bjlbe40q448vyvkyeuo7s2nf7fohp8a3u8x.png)

3. Now, into the **File name** field, as illustrated below, paste **C:Windows\System32\drivers\etc\hosts.tx**t, then click **Open**.

![](https://uploads.developerhub.io/prod/2x2P/h4k1h1cshxti24d33ojq93nf5w0iq1s09z7fjpt3w0ohkcpfn2s3yj05zzp048ii.png)

4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the bottom of the text, as illustrated below, then click **File>Save**.

![](https://uploads.developerhub.io/prod/2x2P/fq2m9la6kqrpwd4ea4li2dix7tpojmy1p2gg4f9tfhbabcqzq8iwyp8b0hnsbg7v.png)

## On macOS devices

1. Launch a **Terminal**.
2. In the command line, type **sudo nano /etc/hosts**, then hit **Enter**.

![](https://uploads.developerhub.io/prod/2x2P/32000nkt8odb6q4q9o0y0zt2eo0zyyjfwgpq9vy71dg5f38bq2rc2rqh09en0hiz.png)

3. Enter your admin **Password** as prompted, then hit **Enter** again.
4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the text, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/oaurzepgxcx6s7q02kgd9a261rff89p8fq09tkuwftzwrq60nzvn48oi71ba7uhc.png)

5. Once added, hit **Ctrl O**, followed by **Enter** to save your changes, then hit **Ctrl X** to exit the nano editor.

## On Linux devices

> **Please note:**
>
> The following steps were recorded in Ubuntu, but interfaces may vary per distro.

1. Launch a **Terminal**.
2. Type **sudo nano /etc/hosts** and then hit **Enter**.

![](https://uploads.developerhub.io/prod/2x2P/gakeftvuqlkb9v6djinf49b84cffe1zkchdd1lsmcks3ad05u3cq21eqi596tmdn.png)

3. Enter your admin **Password**, as prompted.
4. When the **hosts.txt** file opens, add **127.0.0.1 eapi.opswatgears.com** to the top of the text, as illustrated below.

![](https://uploads.developerhub.io/prod/2x2P/fu78qegtp38lmgb81mmg92q9hnv4epcbmtey4wefjy2tjpf4lkyhlmb2bm5qdzfu.png)

5. Once you’ve edited the text, hit **Ctrl X** and then **Y** to save your changes.

> **Support:**
>
> If you have applied this temporary solution but your administrator Is **Unable To Find A Permanent Solution To One Or More Devices Being Unable to Resolve The Cross-Domain API URL**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
