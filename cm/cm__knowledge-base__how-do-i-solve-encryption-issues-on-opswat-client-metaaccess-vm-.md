<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-do-i-solve-encryption-issues-on-opswat-client-metaaccess-vm- -->

# How do I solve encryption issues on MetaDefender Endpoint/My OPSWAT Central Management VM devices using Cryptsetup?

> **Check Your Product:**
>
> This article applies to Linux Cryptsetup, the current My OPSWAT Central Management Console and API, and all MetaDefender Endpoint releases deployed on virtual Linux systems.

Users running MetaDefender Endpoint on one or more Linux virtual devices (VMs) may occasionally see My OPSWAT Central Management device compliance warnings/flags related to encryption.

This warning/flag is triggered by a device issue and will appear under **My OPSWAT Central Management** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**.

> **Pro Tip:**
>
> Cryptsetup is a Linux command line tool that allows users to interface with dm-crypt to create, access and manage encrypted devices and streamline setup of dm-crypt managed device-mapper mappings.
>
> OPSWAT highly recommends that you use this tool to encrypt all unencrypted Linux virtual devices in your My OPSWAT Central Management inventory.

This article covers the process of using Cryptsetup to:

- **Option 1:** encrypt your virtual disk during the Ubuntu install process.
- **Option 2:** encrypt your Home partition following Ubuntu install.

> **Pro Tip:**
>
> Encryption during install is always recommended since it allows full disk encryption that includes swap space and system partitions. Should this not be an option on one or more of your virtual devices, please use **Option 2**.

## Option 1: Encryption During Install

### Phase 1: Initiate Ubuntu installation

1. Boot your new VM via either your computer’s DVD drive, a USB flash drive, your VM installer tool, or an Ubuntu image.

![](https://uploads.developerhub.io/prod/1yda/gsnn7vymk3omsqlw7chh744jgpvlv33k1v8wum28gk40zvrvie101j9h26s10o7e.png)

2. Select your **Language**, then click **Install Ubuntu** on the right-hand side of the screen to start installing the distro.

![](https://uploads.developerhub.io/prod/1yda/gp5fegnlwsud8me8wgvrrf2jbhbr7ofom1apzlujb23kjudpwwa676shnx7gdn9m.png)

3. Select your preferred **Keyboard layout**, then click **Continue**.

![](https://uploads.developerhub.io/prod/1yda/g8wxzripanjlb6nlg9ynfkakss2pa4hxf94xf2lv3gwahyvjemdp0kzqeadzcax9.png)

4. On the **Updates and other software** screen, select how you would like to install Ubuntu. Your options include:
   - **Normal installation**: all features and selected software will be installed.
   - **Minimal installation**:only basic components will be installed, and you can download and install software as required.
   - **Download updates while installing Ubuntu**: auto-download updates while installing, provided you are on a stable, fast internet connection.
   - **Install third-party software for graphics and Wi-Fi hardware and additional media formats**: some license-requiring software, and some proprietary software for graphics, Wi-Fi and additional media formats, will be installed.
5. Click **Continue** to save and proceed.

![](https://uploads.developerhub.io/prod/1yda/h3l4ukwt4sprj1ijzut3es8xoubf47dsbitvemwgjnc5jjchl29i42496rxykr41.png)

### Phase 2: Encrypt Your Disk During Install

1. On the **Installation type** screen of the wizard, select the installation type to be applied to your disk while installing. There are two options:

- **Erase disk and install Ubuntu**: select this option.
- **Something else**: ignore this option.

2. Under the first option above, there are two sub-options that are checked by default and that should remain checked. If they are not checked, ensure that you check them. They are:

- **Encrypt the new Ubuntu installation for security**: select this option.
- **Use LVM with the new Ubuntu installation**: select this option.

3. With the appropriate boxes checked, click the **Install Now** button.

![](https://uploads.developerhub.io/prod/1yda/mh06si8xz51k7agm98fsz5zhfpsqgof531qk1x3tg1akdj0u137x42wj12mt0djm.png)

> **Pro Tip:**
>
> Clicking **Install Now** after selecting encryption options, as you did in the previous steps, will trigger an additional configuration screen on which you will be asked to **Choose a security key**.
>
> Once set up, this key will need to be entered when the virtual machine starts up.

4. Set and confirm a strong **Security Key** that will be entered when the VM starts up.
5. Click **Install Now** to proceed.

![](https://uploads.developerhub.io/prod/1yda/ximyitpcjvhbdxlftirqygd9az0xusbyz7y9o722bkdvx4zagtojf4obywurla6z.png)

6. On the pop-up screen, you should opt to **Overwrite all empty disk space**, then click **Continue** to proceed.

> **Pro Tip:**
>
> This is the most secure option, as all unused disk space will be overwritten by the filesystem, with either random content or zeros.

### Phase 3: Finish the Installation

> **Please Note:**
>
> The following steps are based on typical Ubuntu installation configurations, but the process may vary according to your preferences and  specific version.

1. Select your preferred **Time Zone**.

![](https://uploads.developerhub.io/prod/1yda/4dbdeyxpzmavmp8puzcwdrqpaa3nc9ohbod8qgbld6625s44ridezd4t50v34dam.png)

2. On the **Who are you?** Screen, create a login account and set a hostname for your VM.
3. As an additional layer of security, select the **Require my password to log in** option on this same screen.

> **Pro Tip:**
>
> A login screen will now be shown at each boot up, and you will not be permitted to log in  until you have entered your credentials.

4. On the same page, you should also select the option to **Encrypt my home folder**, as an added layer of security for the data on your system.
5. Click **Continue** to save your settings and begin the installation.

![](https://uploads.developerhub.io/prod/1yda/ifvgpexw0401ryapewzqye7g1km81hnby79fa2w1yedn0we9jpjpsew8m1d2t5m2.png)

6. Finally, click the **Restart Now** button on the pop-up to restart your system and complete the installation.

![](https://uploads.developerhub.io/prod/1yda/ozb9wpp6nbhh5uthsn5lx59t1a57bb28cg0vjwb5ujvjqstcqknvhxzxg6caqv8j.png)

> **Please Note:**
>
> Once this system starts, you will be prompted to enter the security key that you set up in Step 4 of Phase 2 above.
>
> Without this encryption-passkey, the system will not boot - and there is no way to bypass it.

![](https://uploads.developerhub.io/prod/1yda/077bqbnfyzrwkbn653gl1ayyea34j64xeqyy0ij7ndztzdixw37o1tuib8c2jqo8.png)

### Phase 4: Verify That the Disk Is Encrypted

1. Log into the system by entering the **Credentials** that you set up during Phase 3 above, then clicking **Sign In**.

![](https://uploads.developerhub.io/prod/1yda/3zro72nbxcwok8pg6k5c1w3u1dq9gx1dgnlyexpxmvlvpjp2it3r38rj545ira7x.png)

2. Once you’re logged in, open a **Terminal** and run the following command to check your encryption status: **$lsblk -o NAME,MOUNTPOINT,TYPE,FSTYPE**

```bash
$lsblk -o NAME,MOUNTPOINT,TYPE,FSTYPE
```

3. In the response, check the file system type of a given partition. If it is listed as **crypto_LUKS** for the **FSTYPE**, this means the partition is encrypted.

![](https://uploads.developerhub.io/prod/1yda/2h3saelbzolackjia54ydlaz7ng0ahg9zx7n1divz4b5zvnj669jpy3fpibsdc9q.png)

> **Pro Tip:**
>
> To learn more about disk encryption in Ubuntu, please [Read This](https://www.maketecheasier.com/encrypt-hard-disk-in-ubuntu/).
>
> For guidelines on installing Ubuntu via VM Workstation, [Read This](https://getlabsdone.com/10-easy-steps-to-install-ubuntu-19-04-on-vmware-workstation-15/). For guidelines on installing Ubuntu via Virtualbox, [Read This](https://www.shaileshjha.com/how-to-install-ubuntu-desktop-in-virtualbox/).

## Option 2: Encryption of the Home Partition Following Install

> **Pro Tip:**
>
> Before undertaking this process, you should back up your home directory and important files.
>
> The migration command will create a backup of your data, but it’s advised that you take extra precautions, just in case something goes wrong.

> **Please Note:**
>
> The following guideline demonstrates the process to encrypt a home partition for the user named **test**, with the user running their migration as the newly created **tempuser**.
>
> This guideline was prepared on Ubuntu 19.10 and Ubuntu 18.4, and the process may vary slightly from version to version.

### Phase 1: Install the Encryption Utilities

1. Open a **Terminal** and run the following command to install the encryption utilities: **sudo apt-get install ecryptfs-utils cryptsetup**

```plaintext
sudo apt-get install ecryptfs-utils cryptsetup
```

![](https://uploads.developerhub.io/prod/1yda/uugvgrz1rb7cd366kksrwxu1pm0y1qayedmzslgasorpuxobd2bububney49wf6c.png)

![](https://uploads.developerhub.io/prod/1yda/ybdts4nfbwxwdgu1e4ati7f4p7uasdtzflxxia6nkz0t0qualzsh0qht8jgbqo6r.png)

![](https://uploads.developerhub.io/prod/1yda/lxh5c8waaf4caxay1y18skdyuictu6aot6a5c7s6lv7a86idlqk2aay1vd9bx8vc.png)

### Phase 2: Create a New User Account With Administrator Privileges

1. Open a terminal and run the following command to create a user account, named **tempuser**

```bash
sudo adduser tempuser
sudo usermod -aG sudo tempuser
```

![](https://uploads.developerhub.io/prod/1yda/zklarnmgo0f7e0u3q4cjf6xulcu9xwzi6igvz2v2zc9xdqcqsxuutaba87jpguuc.png)

2. Log out, then log in again with the newly created user, **tempuser**.

![](https://uploads.developerhub.io/prod/1yda/2dlp4f1l6lka6xqbkffljxvi3ptf8y42oocv8j0cz4lnqi3qhmnq2p86rhri0n40.png)

### Phase 3: Migrate the Same Home Folder That You Wish To Encrypt

> **Please Note:**
>
> It is essential that you log in as an administrator user, but *not* the user who’s Home partition you would like to encrypt.

Open a **Terminal**, then run the following command to migrate the Home partition of the user named **test**, the same Home partition you plan to encrypt:

```bash
sudo ecryptfs-migrate-home -u test
```

### Phase 4: Log Into The Account for Which the Home Partition Is To Be Encrypted

1. Log out and log back in again as the user who’s Home partition will be encrypted - in this case, **test**.

![](https://uploads.developerhub.io/prod/1yda/yy0vvpcqb0cwbv59ni97dfpw5si1r7vw0ms6j6fq7ey3ao5ktos3tzkobqodpg7j.png)

2. Once you are logged in, click the **Run this action now** button to create a recovery **Passphrase**. Store this passphrase safely, as you will need it if you ever have to recover files manually in future.

![](https://uploads.developerhub.io/prod/1yda/vqpmtjl9sdyqg3kmwi7ei4jub7umupbjkh5wa86w3a312spldo7rws6xderhyvyq.png)

![](https://uploads.developerhub.io/prod/1yda/18f0zs77itnjw9lke2ioxa1wajte6t4u19kjjpxyj2537hgfw8nzy0sb62e00ju2.png)

### Phase 5: Verify That the Home Partition Is Encrypted

1. Open a **Terminal** and run the following command to verify the encryption status of your Home partition: **ls -A /home**

```plaintext
ls -A /home
```

If your home folder has been encrypted, you will see a **.ecryptfs** folder in the response.**Reference:**

![](https://uploads.developerhub.io/prod/1yda/od31zvdtwzmddlp66ci35g2hakuo63cibqtovbakw5oi62gtgfnb9mxhtfhpib03.png)

> **Pro Tip:**
>
> For further guidelines on encrypting your home folder after installing Ubuntu, [Read This](https://www.howtogeek.com/116032/how-to-encrypt-your-home-folder-after-installing-ubuntu/) and [This](https://www.linuxuprising.com/2018/04/how-to-encrypt-home-folder-in-ubuntu.html).

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Encryption Issues On Your MetaDefender Endpoint/ My OPSWAT Central Management** **Virtual Devices**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
