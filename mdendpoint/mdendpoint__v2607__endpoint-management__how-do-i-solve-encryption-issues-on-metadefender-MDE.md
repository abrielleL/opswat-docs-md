<!-- source: https://www.opswat.com/docs/mdendpoint/v2607/endpoint-management/how-do-i-solve-encryption-issues-on-metadefender-MDE -->

# How do I solve encryption issues on MetaDefender Endpoint/MetaDefender IT-OT Access VM devices using Cryptsetup?

> **Check Your Product:**
>
> This article applies to Linux Cryptsetup, the current MetaDefender IT-OT Access Console and API, and all MetaDefender Endpoint releases deployed on virtual Linux systems.

Users running MetaDefender Endpoint on one or more Linux virtual devices (VMs) may occasionally seeMetaDefender IT-OT Access device compliance warnings/flags related to encryption.

This warning/flag is triggered by a device issue and will appear under **MetaDefender IT-OT Access** **Console>Inventory>Devices>Relevant Device>Detailed Device Information>Deep Compliance>Encryption**.

> **Pro Tips:**
>
> Cryptsetup is a Linux command line tool that allows users to interface with dm-crypt to create, access and manage encrypted devices and streamline setup of dm-crypt managed device-mapper mappings.
>
> OPSWAT highly recommends that you use this tool to encrypt all unencrypted Linux virtual devices in your MetaDefender IT-OT Access inventory.

This article covers the process of using Cryptsetup to:

- **Option 1:** encrypt your virtual disk during the Ubuntu install process.
- **Option 2:** encrypt your Home partition following Ubuntu install.

> **Pro Tips:**
>
> Encryption during install is always recommended since it allows full disk encryption that includes swap space and system partitions. Should this not be an option on one or more of your virtual devices, please use **Option 2**.

## Option 1: Encryption During Install

### Phase 1: Initiate Ubuntu installation

1. Boot your new VM via either your computer’s DVD drive, a USB flash drive, your VM installer tool, or an Ubuntu image.

![](https://uploads.developerhub.io/prod/2x2P/x3d3xx1pbbcfx1ggs0iy9d9w47s6i8c8up7kx9djn3cgbvfg7cwcy7sevp1j4zyz.png)

2. Select your **Language**, then click **Install Ubuntu** on the right-hand side of the screen to start installing the distro.

![](https://uploads.developerhub.io/prod/2x2P/ae9z326lvd4a5n2c1z6mybibbsr1ndchy94yl5tfmx5tpock5ilsct1td6xzvv36.png)

3. Select your preferred **Keyboard layout**, then click **Continue**.

![](https://uploads.developerhub.io/prod/2x2P/w1terujix6e2notacle9rlrjmz4yydmo66tmdkp8hanzr3bpso1hy01a48mjzii2.png)

![](https://uploads.developerhub.io/prod/2x2P/5huijzb7axsoatrf4u32rnqa6ycw7twou4pv9a2iqzpfzldoug678q7zbkqtwaq0.png)

4. On the **Updates and other software** screen, select how you would like to install Ubuntu. Your options include:
   - **Normal installation**: all features and selected software will be installed.
   - **Minimal installation**:only basic components will be installed, and you can download and install software as required.
   - **Download updates while installing Ubuntu**: auto-download updates while installing, provided you are on a stable, fast internet connection.
   - **Install third-party software for graphics and Wi-Fi hardware and additional media formats**: some license-requiring software, and some proprietary software for graphics, Wi-Fi and additional media formats, will be installed.
5. Click **Continue** to save and proceed.

![](https://uploads.developerhub.io/prod/2x2P/6ls4ucyert03eshucm1x58b8olxkd7b32vadua9defnebc7jtfsane8ux2ciegok.png)

### Phase 2: Encrypt Your Disk During Install

1. On the **Installation type** screen of the wizard, select the installation type to be applied to your disk while installing. There are two options:

- **Erase disk and install Ubuntu**: select this option.
- **Something else**: ignore this option.

2. Under the first option above, there are two sub-options that are checked by default and that should remain checked. If they are not checked, ensure that you check them. They are:

- **Encrypt the new Ubuntu installation for security**: select this option.
- **Use LVM with the new Ubuntu installation**: select this option.

3. With the appropriate boxes checked, click the **Install Now** button.

![](https://uploads.developerhub.io/prod/2x2P/o7t9l0yxwuyas37h4qfkcpakdlzi1yhr568humgu406l4dnhdq0y0wqe5gmej00u.png)

> **Pro Tips:**
>
> Clicking **Install Now** after selecting encryption options, as you did in the previous steps, will trigger an additional configuration screen on which you will be asked to **Choose a security key**.
>
> Once set up, this key will need to be entered when the virtual machine starts up.

4. Set and confirm a strong **Security Key** that will be entered when the VM starts up.
5. Click **Install Now** to proceed.

![](https://uploads.developerhub.io/prod/2x2P/tsxqga28hl7wv3517h9d05unq4t8jw407inz85fk2powtr8778sp8dyxm841cv7a.png)

6. On the pop-up screen, you should opt to **Overwrite all empty disk space**, then click **Continue** to proceed.

> **Pro Tips:**
>
> This is the most secure option, as all unused disk space will be overwritten by the filesystem, with either random content or zeros.

### Phase 3: Finish the Installation

> **Please Note:**
>
> The following steps are based on typical Ubuntu installation configurations, but the process may vary according to your preferences and specific version.

1. Select your preferred **Time Zone**.

![](https://uploads.developerhub.io/prod/2x2P/9ip309o29wyfv17pt02rtwuym7nfh84ggu7edcpb1mj5yvamcpzjabmu9tadisi4.png)

2. On the **Who are you?** Screen, create a login account and set a hostname for your VM.
3. As an additional layer of security, select the **Require my password to log in** option on this same screen.

> **Pro TIps:**
>
> A login screen will now be shown at each boot up, and you will not be permitted to log in until you have entered your credentials.

4. On the same page, you should also select the option to **Encrypt my home folder**, as an added layer of security for the data on your system.
5. Click **Continue** to save your settings and begin the installation.

![](https://uploads.developerhub.io/prod/2x2P/rcs1wtslrbd56oj727tlxp8lxifh975y29h7rd5ixi2rkzx4zmyca188f2tw6t50.png)

6. Finally, click the **Restart Now** button on the pop-up to restart your system and complete the installation.

![](https://uploads.developerhub.io/prod/2x2P/azhqmkn2txfhqvdlazexyqzr1psycenwd7bddfov7yrt8q1mdba7vhy8ctk8p4km.png)

> **Please Note:**
>
> Once this system starts, you will be prompted to enter the security key that you set up in Step 4 of Phase 2 above.
>
> Without this encryption-passkey, the system will not boot - and there is no way to bypass it.

![](https://uploads.developerhub.io/prod/2x2P/kondj5kf4lre89of1lqiqdopsqr7nclw09zjnharj0bobvjbz23l529anb4bzlp0.png)

### Phase 4: Verify That the Disk Is Encrypted

1. Log into the system by entering the **Credentials** that you set up during Phase 3 above, then clicking **Sign In**.

![](https://uploads.developerhub.io/prod/2x2P/jfowxfrdr69x89dvh8suhjlmn9qf2wjqkp1hu64q0t9tzr3v4tzehdwd46k12gas.png)

2. Once you’re logged in, open a **Terminal** and run the following command to check your encryption status: **$lsblk -o NAME,MOUNTPOINT,TYPE,FSTYPE**

```bash
$lsblk -o NAME,MOUNTPOINT,TYPE,FSTYPE
```

3. In the response, check the file system type of a given partition. If it is listed as **crypto_LUKS** for the **FSTYPE**, this means the partition is encrypted.

![](https://uploads.developerhub.io/prod/2x2P/x5u3yik06u807iq4eur1hzrno9zos5k0vi2uh5ubb6fb3et8k0hm2vhkp3mhqb7h.png)

> **Pro Tips:**
>
> To learn more about disk encryption in Ubuntu, please [Read This](https://www.maketecheasier.com/encrypt-hard-disk-in-ubuntu/).
>
> For guidelines on installing Ubuntu via VM Workstation, [Read This](https://getlabsdone.com/10-easy-steps-to-install-ubuntu-19-04-on-vmware-workstation-15/). For guidelines on installing Ubuntu via Virtualbox, [Read This](https://www.shaileshjha.com/how-to-install-ubuntu-desktop-in-virtualbox/).

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

![](https://uploads.developerhub.io/prod/2x2P/yxm060i0ahmcx0wo63xc3qmq0iqe9t8p31t0q0nzbh4eptju026rtd5jbvbxaoog.png)

2. Log out, then log in again with the newly created user, **tempuser**.

![](https://uploads.developerhub.io/prod/2x2P/j573ypmtvafq1qjk58dw7rwyrdcaj7grligtcvjns0qyr8zl6k0aj9u2q77osrbt.png)

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

![](https://image-archive.developerhub.io/image/upload/v2_5265/f9nwjtzvpejpfwtiqjfh/1628792616.png)

2. Once you are logged in, click the **Run this action now** button to create a recovery **Passphrase**. Store this passphrase safely, as you will need it if you ever have to recover files manually in future.

![](https://uploads.developerhub.io/prod/2x2P/0kh5e6rmgam6oj7yfzh319webp9ievzbumfjwgkmdxi453s7y7uejia29qeh1mn0.png)

![](https://uploads.developerhub.io/prod/2x2P/v59fibwpvhb2da81sfyjku0vtqxe9o0epyqabx5tu4qrgo9d94np9jcd3ac8i1ed.png)

### Phase 5: Verify That the Home Partition Is Encrypted

1. Open a **Terminal** and run the following command to verify the encryption status of your Home partition: **ls -A /home**

```bash
ls -A /home
```

If your home folder has been encrypted, you will see a **.ecryptfs** folder in the response.

**Reference:**

![](https://uploads.developerhub.io/prod/2x2P/gea4oxdc01u4uwtnaqrik3elqwlwd280zhqylpbx2bbj84u5rv0n39xanlnsn7ld.png)

> **Pro Tips:**
>
> For further guidelines on encrypting your home folder after installing Ubuntu, [Read This](https://www.howtogeek.com/116032/how-to-encrypt-your-home-folder-after-installing-ubuntu/) and [This](https://www.linuxuprising.com/2018/04/how-to-encrypt-home-folder-in-ubuntu.html).

> **Support:**
>
> If you have followed the instructions above but **Continue To Experience Encryption Issues On Your MetaDefender Endpoint/ MetaDefender IT-OT Access** **Virtual Devices**, please open a [Support Case](https://www.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go.opswat.com/OPSWATCommunity/s/).
