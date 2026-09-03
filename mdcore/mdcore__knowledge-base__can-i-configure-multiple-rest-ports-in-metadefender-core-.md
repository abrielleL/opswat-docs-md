<!-- source: https://www.opswat.com/docs/mdcore/knowledge-base/can-i-configure-multiple-rest-ports-in-metadefender-core- -->

# Can I configure multiple REST ports in MetaDefender Core?

This article applies to all MetaDefender Core releases deployed on Windows and Linux systems.

**Overview:**

MetaDefender Core supports only **one** REST port per instance for API calls and web access. Configuring multiple REST ports on the same MetaDefender Core installation is not supported.

**Steps to Configure the REST Port:**

The REST/web console port can be configured as described in this article: <https://www.opswat.com/docs/mdcore/knowledge-base/how-to-change-core-web-management-interface-address-port-#windows>

**How to Verify the Change:**

- Check that the REST API and web console are accessible on the specified port after restarting the MetaDefender Core service.

Support:

If **Further Assistance** is required, please proceed to log a [support case or chat with our support engineer](https://my.opswat.com/support).
