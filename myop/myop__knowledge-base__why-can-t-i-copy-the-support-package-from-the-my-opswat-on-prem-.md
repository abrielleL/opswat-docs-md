<!-- source: https://www.opswat.com/docs/myop/knowledge-base/why-can-t-i-copy-the-support-package-from-the-my-opswat-on-prem- -->

# Why can't I copy the support package from the My OPSWAT On-Prem product?

**Issue:**

A support package was generated for the My OPSWAT On-Prem product following the steps outlined in the article below:

[Support package creation steps](https://www.opswat.com/docs/myop/knowledge-base/how-to-generate-a-support-package-for-troubleshooting)

However, when attempting to copy the generated file using the scp tool, the following error was encountered:

**scp: Connection closed**

**Solution:**

Try using the scp command with the -O flag:

scp -O [user@host:/path/to/support-package.tar.gz](mailto:user@host:/path/to/support-package.tar.gz)

The -O option forces the use of the legacy SCP protocol instead of SFTP, which is the default in newer OpenSSH versions. This resolves the connection issue when transferring files from My OPSWAT On-Prem.

Support:

If you encounter any issues during the activation process or require further assistance, please contact OPSWAT support via My OPSWAT at: https://my.opswat.com/home

Our support team will be able to provide you with the necessary guidance and resolution for any license-related concerns.
