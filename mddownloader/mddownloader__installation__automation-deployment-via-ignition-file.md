<!-- source: https://www.opswat.com/docs/mddownloader/installation/automation-deployment-via-ignition-file -->

# Automation deployment via ignition file

From version 3.3.0, users can setup automation deployment via ignition file

## [Overview](/docs/mddownloader/installation/automation-deployment-via-ignition-file#overview)

The ignition file is a configuration file that enables automated deployment and configuration of the Update Downloader system. It allows you to pre-configure settings, create admin users, add products, and set up post-installation actions without manual intervention through the web interface.

Location

- Windows: `C:\opswat\ometadownloader.conf`
- Linux: `/etc/opswat/ometadownloader.conf`

### [File Format](/docs/mddownloader/installation/automation-deployment-via-ignition-file#file-format)

The ignition file uses INI format with sections and key-value pairs. The file should be named appropriately and placed in the correct location where the system can detect it during startup.

## [Complete Example](/docs/mddownloader/installation/automation-deployment-via-ignition-file#complete-example)

ometadownloader.confCopyeula=true
[user]
name=admin
password=admin
email=admin@local
apikey=user_apikey_36_characters
[update_settings]
interval=15
packagelocation=C:/Program Files/OPSWAT/Metadefender Update Downloader/data/update_packages
cleanup=4
exclude=Monday-Friday 08:15-16:15
exclude_1=Saturday 13:00-23:59
exclude_2=Sunday 00:00-11:00
[post_action]
name=ps_python
command=D:/post action/post.py
[post_action_1]
name=ps_binary
command=D:/post action/post.exe
product_name=MetaDefender Core A
product_name_1=MetaDefender Core B
[product]
name=MetaDefender Core A
license=E:/opswat/Core_licenses/md_core_a_license_file.yml
[product_1]
name=MetaDefender Core B
license=E:/opswat/Core_licenses/md_core_b_license_file.yml
## [Details Configuration](/docs/mddownloader/installation/automation-deployment-via-ignition-file#details-configuration)

### [EULA Acceptance - Required](/docs/mddownloader/installation/automation-deployment-via-ignition-file#eula-acceptance---required)

The EULA (End User License Agreement) must be accepted for the ignition file to be processed:

BashCopyeula=true

**Note:** This is a required field. The ignition file will not be processed if this is not set to `true`.

## [User Configuration - Optional](/docs/mddownloader/installation/automation-deployment-via-ignition-file#user-configuration---optional)

You can automatically create an admin user during deployment:

BashCopy[user]
name=admin
password=admin
email=admin@local
apikey=user_apikey_36_characters
### [User Fields:](/docs/mddownloader/installation/automation-deployment-via-ignition-file#user-fields)

- `name`: Username for the admin account
- `password`: Password for the admin account
- `email`: Email address for the admin account
- `apikey`: (Optional) API key for the user

**Note:** If you provide user information, all fields except `apikey` are required.

## [Update Settings Configuration - Optional](/docs/mddownloader/installation/automation-deployment-via-ignition-file#update-settings-configuration---optional)

Configure automatic update settings for the Update Downloader:

BashCopy[update_settings]
interval=15
packagelocation=C:/Program Files/OPSWAT/Metadefender Update Downloader/data/update_packages
cleanup=4
exclude=Monday-Friday 08:15-16:15
exclude_1=Saturday 13:00-23:59
exclude_2=Sunday 00:00-11:00
### [Update Settings Fields - Optional](/docs/mddownloader/installation/automation-deployment-via-ignition-file#update-settings-fields---optional)

#### [interval](/docs/mddownloader/installation/automation-deployment-via-ignition-file#interval)

Auto-update interval in minutes. Valid values:

- `0` - Disabled
- `15` - 15 minutes
- `30` - 30 minutes
- `60` - 1 hour
- `120` - 2 hours
- `240` - 4 hours (default)
- `360` - 6 hours
- `720` - 12 hours
- `1440` - 24 hours

#### [cleanup](/docs/mddownloader/installation/automation-deployment-via-ignition-file#cleanup)

Cleanup interval in hours. Valid values:

- `0` - Disabled
- `1` - 1 hour
- `4` - 4 hours
- `12` - 12 hours
- `24` - 24 hours (default)
- `168` - 1 week
- `672` - 4 weeks

#### [packagelocation](/docs/mddownloader/installation/automation-deployment-via-ignition-file#packagelocation)

Directory path where update packages will be stored. The system will create this directory if it doesn't exist and verify write permissions.

#### [exclude](/docs/mddownloader/installation/automation-deployment-via-ignition-file#exclude)

Time periods when updates should be disabled. Format options:

- Single day: `Monday 08:00-17:00`
- Day range: `Monday-Friday 08:00-17:00`

Valid day ranges:

- `Monday-Friday`
- `Friday-Sunday`
- `Sunday-Thursday`

You can specify multiple exclude periods using numbered suffixes (`exclude_1`, `exclude_2`, etc.). Maximum 100 excludes

## [Post-Action Configuration - Optional](/docs/mddownloader/installation/automation-deployment-via-ignition-file#post-action-configuration---optional)

Configure commands to run after product installation:

Users can add maximum 100 items for Post-Action, the first one should be `post_action`

If user want to add more Post-Action, using this pattern: "post_action_1" , "post_action _2", etc

BashCopy[post_action]
name=ps_python
command=D:/post action/post.py
[post_action_1]
name=ps_binary
command=D:/post action/post.exe
product_name=MetaDefender Core A
product_name_1=MetaDefender Core B
### [Post-Action Fields:](/docs/mddownloader/installation/automation-deployment-via-ignition-file#post-action-fields)

- `name`: Action name (maximum 16 characters, must be unique)
- `command`: Command to execute
- `product_name`: Product name that triggers this action (can have multiple using numbered suffixes)
- We can add multiple products to a Post-Action: product_name_1, product_name_2, etc. Maximum 100 products

**Note:** Actions are triggered when the associated products are installed.

## [Product Configuration - Optional](/docs/mddownloader/installation/automation-deployment-via-ignition-file#product-configuration---optional)

Add products with their licenses during deployment:

BashCopy[product]
name=MetaDefender Core A
license=E:/opswat/Core_licenses/md_core_a_license_file.yml
[product_1]
name=MetaDefender Core B
license=E:/opswat/Core_licenses/md_core_b_license_file.yml
### [Product Fields:](/docs/mddownloader/installation/automation-deployment-via-ignition-file#product-fields)

- `name`: Product name - **must be unique** between product fields
- `license`: The absolute path to the license file

**Note:** Both fields are required for each product section.

## [Limitations](/docs/mddownloader/installation/automation-deployment-via-ignition-file#limitations)

- Maximum 100 items for repeated sections (product, product_name, post-action, exclude)
- Post-action names limited to 16 characters
- Package location must be writable by the system
- License files must be accessible during processing
- Time exclusions must follow exact format specifications
