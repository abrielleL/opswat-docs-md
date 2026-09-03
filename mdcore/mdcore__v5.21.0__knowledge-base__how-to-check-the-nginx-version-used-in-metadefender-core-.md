<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/knowledge-base/how-to-check-the-nginx-version-used-in-metadefender-core- -->

# How to check the Nginx version used in MetaDefender Core?

This article applies to all MetaDefender Core releases deployed on Windows, Linux.

### [**Overview:**](/docs/mdcore/v5.21.0/knowledge-base/how-to-check-the-nginx-version-used-in-metadefender-core-#overview)

This article explains how to determine the Nginx version used in your current MetaDefender Core installation.

### [**On Windows:**](/docs/mdcore/v5.21.0/knowledge-base/how-to-check-the-nginx-version-used-in-metadefender-core-#on-windows)

1. Open Terminal (Command Prompt or PowerShell).
2. Navigate to the MetaDefender Core installation folder, specifically to the nginx subfolder: `cd "C:\Program Files\OPSWAT\MetaDefender Core\nginx"`
3. Run the following command: `nginx.exe -v`

### [**On Linux:**](/docs/mdcore/v5.21.0/knowledge-base/how-to-check-the-nginx-version-used-in-metadefender-core-#on-linux)

1. Go to the `/usr/lib/ometascan/` directory.
2. Run the following command: `./nginx -v`

### [**Verify the Change:**](/docs/mdcore/v5.21.0/knowledge-base/how-to-check-the-nginx-version-used-in-metadefender-core-#verify-the-change)

The command will output the Nginx version. For example: `nginx version: nginx/1.26.2`

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
