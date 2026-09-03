<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/configuration-tool -->

# Configuration Tool

**MetaDefender Endpoint Standalone Configuration Tool** is used to empower administrators to pre-configure settings for the MetaDefender Endpoint Standalone. Administrators will utilize this tool to select the following settings:

- Installer file with a filename containing password information
- Certificate file for validation purposes.
- Encrypted configuration file containing configuration details including:
  - Enable or disable Bad USB Protection
  - Enable or disable allow list device
  - List of allow vendor name
  - List of allow product ID
  - List of allow regex with instance path
  - The number of days to trust Media Manifest.

## Create a folder containing all necessary information for deployment

- **Step 1:** Enter and re-enter the password for the installer file.

![If you leave this section blank, the tool will use the default password `Opswat1234!` instead.](https://uploads.developerhub.io/prod/2x2P/ejqp8gnredvkbbqiiklwuqmsj787lvnmjxhx5q07m695lugr6kvsgn4pxmsxz065.png)

- **Step 2**: Select the installation file that uses the password above.

![](https://uploads.developerhub.io/prod/2x2P/f9wrexcn5oqqfn2hmebeqhqgwi8opd6401y1shglxm6076xfkb0sep3118x573dz.png)

- **Step 3:** Select the certificate file and enter the number of days to trust Media Manifest. MetaDefender Endpoint will not use any Media Manifest older than this many days.

![The default number of days is 7. The adjustment range is 1 to 60 days.](https://uploads.developerhub.io/prod/2x2P/vcc61f1dfn8pgcjwnt22znzvg487trf5pirofe29y8zxxhubpl041uj6b730s4gt.png)

- **Step 4:** Configuration Bad USB Protection. Check for enable or uncheck for disable Bad USB Protection. Default is enabled.

![](https://uploads.developerhub.io/prod/2x2P/i5ic5by2x3kss5eohabo5sywwk95ag872m41jsr6pr1iaymhgw23ljmj3u9weyvr.png)

- **Step 5**: Configuration allows list devices. You need to click "Enable allowlist devices" to see and enter the devices that need to be allowed.

![](https://uploads.developerhub.io/prod/2x2P/dsqissz66xhjik6cv02sts73mnqv7eynd2o17xitfm5hy3r4coyozh7ebq58j9df.png)

> **Info**
>
> When you select **"All Devices Information"**, you will be able to view all current drives information. You can rely on that to accurately enter the drive information you need to allow. You can click the icon after the drive information to copy it to the clipboard or rescan to update list of device information.

![](https://uploads.developerhub.io/prod/2x2P/kytvljpz66iwndvp62lv59g2e43mk2fs8lr4vem2t95b2xh3dk4talne2c85z6pp.png)

- **Step 6:** Select the destination path and generate.

![](https://uploads.developerhub.io/prod/2x2P/439qa6snkcv2oqasln53wlnnvfaclyr2rvy0tzz93n480b7l93974vbn2vtrvtj4.png)

## Load an encrypted configuration file

Click the load config button and select the config file you want to load. When you click Open button all information in the config will be overwritten in the current workspace. Note that installer file path, certificate file path, output folder, and password not in the config file and they will retain the same value after loading the config.

![](https://uploads.developerhub.io/prod/2x2P/3jdr6t8qmy3uf6nn38ljh14o5ce2hwzovqyum8lg3wpaklh8e53q292dxu2sx1lf.png)
