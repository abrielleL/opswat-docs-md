<!-- source: https://www.opswat.com/docs/cm/knowledge-base/resolved-os-patch-ubuntu-mde -->

# How do I solve Missing OS Patch issues on MetaDefender Endpoint/My OPSWAT Central Management managed Ubuntu Linux devices?

> **Check Your Product:**
>
> This article applies to the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on Ubuntu Linux systems.

My OPSWAT Central Management provides variety compliance options tailored to different operating systems. Specifically for Ubuntu devices, we've implemented a dedicated rule aimed at compelling users to regularly update their operating systems. This involves monitoring the current patching status and detecting any available but uninstalled updates. This proactive approach ensures that the system remains current, benefiting from the latest enhancements and security patches, ultimately bolstering device stability and security.

Administrators have the flexibility to determine the frequency at which users are prompted to update their operating system. This can be configured by activating the '**Update(s) have been available**' condition under **Policy > Deep Compliance > Operating System > Linux**, allowing administrators to specify the desired update interval in days. A smaller number indicates a more frequent check for operating system updates.

![](https://uploads.developerhub.io/prod/1yda/9s0dbjvnb7t5w66t7qfufmpy6889mqrch3ykghel975mnnse780ixnuhhli99zw2.png)

To remediate OS update compliance issues on managed Ubuntu Linux devices, please follow the relevant instructions below.

> **Warning**
>
> These instructions are based on Ubuntu 20.04.05 LTS and will vary slightly depending on your Ubuntu version.

## Through Software Updater

1. Go to Applications, search for Software Updater, then click on the result.

![](https://uploads.developerhub.io/prod/1yda/ngkcygz299fxp00t75w8k2ot2o4wwwcppcczyh74v3ij4p6gdfxfz03weojy14bn.png)

The Software Updater will initially search for available updates and then display a list of them with checkboxes. You can uncheck any updates you do not want. To update everything, simply leave all the checkboxes checked.

2 . Click “Install now“ once you are satisfied with the selections.

![](https://uploads.developerhub.io/prod/1yda/u6gqpry76aet005xgwmgcz0mlnzsxqwq01y9prrco6nvzhffuee96vt7qaobi52j.png)

Authentication, and the installation will begin.

![](https://uploads.developerhub.io/prod/1yda/324bl9ldkvyp1il5488e1alby5eknz1rroxk1w1d5nagjfv42hybmzrgtprysrx6.png)

![](https://uploads.developerhub.io/prod/1yda/0w7stnd7knr6giupva724vsm85u02a4eq0yh18c7538g85wt48zqgcg0v87f2h16.png)

This process may take some time, and you might be prompted to reboot your machine once it's finished.

## Through Terminal

1. Open terminal and enter the following command to check for updates.

```bash
sudo apt update
```

![](https://uploads.developerhub.io/prod/1yda/lp7kz28etb0aquwmc5t47pswnknokvkf9f9f8c3uba34ygm5y56nv578vm70xxkh.png)

2. Then, execute the flowing command to apply package updates and patches.

![](https://uploads.developerhub.io/prod/1yda/alkiv8vaf4ckp2h5mbg289f11fb2ahwx7j9kl7dcvglgk0h08aoh143pa555cdf3.png)

Type `Y` and press Enter to confirm.

![](https://uploads.developerhub.io/prod/1yda/z1o30qcaqmfkou6px5isnsko2ctejtrvgumgshxlgvahx41dh8d34j5dog27t2wz.png)

## Verify the update with MetaDefender Endpoint

Once the installation is done, ensure that MetaDefender Endpoint is launched. Then, right-click on the MetaDefender Endpoint tray **Icon** and click **Recheck**.

![](https://uploads.developerhub.io/prod/1yda/ytlpikudadrc4hqrjpub55nekl8urq9qih0ynqvv68l6tysqb1tjibu4fha17dtg.png)

> **Support:**
>
> If you have followed the relevant guidelines but **Continue To Experience Missing OS Patch Issues On Your** **MetaDefender Endpoint/My OPSWAT Central Management** **Managed Ubuntu Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
