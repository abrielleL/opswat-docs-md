<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/how-to-move-the-location-of-the-metadefender-storage-security-se -->

# How to move the location of the MetaDefender Storage Security services_logs folder?

> **Check Your Version:**
>
> This article applies to all versions of MetaDefender Storage Security Linux deployments.

## **Background**

When dealing with disk space issues related to the logging created by MDSS in environments where MDSS default log partition might be highly restricted, MDSS supports the ability to use symlinks to point the logs folder to a different partition/location.

## **Steps**

The following provides steps on how to add a symlink for the `/etc/mdss/services_logs` directory/folder:

1. **Change name of the current services_logs folder and it backup**

   ```bash
   sudo mv services_logs/ services_logs_v1/
   ```
2. **Create a symlink:**

   ```bash
   sudo ln -s [absolute_path_to_destination_folder]/services_logs [MDSS_dicretory]
   example: sudo ln -s /home/opswat/MDSS_LOGS/services_logs /etc/mdss/
   ```
3. Restart MDSS:

   ```bash
   sudo mdss -c restart
   ```
4. Once the product restarts, you will be able to see the symlink created by executing the command: `ls -al`. Sample symnlink created shown below:

   ![](https://uploads.developerhub.io/prod/k8zL/zmj5ys71034oxf6ribjtk8vtl54rftz1ykma9e09ko3rqp7oanpxgvl3uy6ubznq.png)

> Notes:
>
> After restart, a new file structure and logs will be created on the destination of the symlink.
>
> Further restarts of MDSS will not affect symlink functionality.

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
