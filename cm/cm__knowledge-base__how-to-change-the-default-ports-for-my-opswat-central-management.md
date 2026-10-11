<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-to-change-the-default-ports-for-my-opswat-central-management -->

# How to change the default ports for My OPSWAT Central Management v10 on Windows

> **Check Your Version:**
>
> This article applies to all MyOPSWAT Central Management v10 releases deployed on Windows systems.

## **Overview**

By default, My OPSWAT Central Management serves its web management console on port **9000**. In some environments this port is already in use by another service, or organizational policy requires a different listening port.

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MOCM`

---

## **How To:**

### **Prerequisites**

- Administrator access to the Windows machine running My OPSWAT Central Management
- Access to the Windows Registry Editor (regedit)
- The new port must be free on the server, and must not fall inside the internal range 30000–30071

### **Steps**

1. **Stop the My OPSWAT Central Management service**

Open the Windows Services panel (`services.msc`), locate the **My OPSWAT Central Management** service, and stop it.

2. **Back up the registry key**

Open Registry Editor (**Win + R**, type `regedit`, press **Enter**), right-click `Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MOCM`, select **Export**, and save a copy. This lets you restore the previous configuration if the service does not start.

3. **Navigate to the My OPSWAT Central Management registry key**

Go to:

`Computer\HKEY_LOCAL_MACHINE\SOFTWARE\OPSWAT\MOCM`

4. **Update the port value**

Double-click **NginxPort** and enter the new port number. This is the main service port, used by the web management console and by the managed product instances.

Default value: `9000`

If **IsUIPortSeparate** is set to `Yes` on your installation, the administration console runs on its own port. In that case, update **UIPort** as well.

5. **Restart the My OPSWAT Central Management service**

Return to the Windows Services panel and start the service. Allow a few minutes for it to fully initialize.

6. **Verify the new port**

Open the web management console at the new address:

`https://<server_address>:<new_port>`

---

## **Port and networking values in the registry key**

### **Values an administrator can change**

| Registry value | Purpose | Default |
| ---- | ---- | ---- |
| `NginxPort` | Main service port, used by the web management console and by managed product instances | `9000` |
| `UIPort` | Administration console port, used only when the console port is separated | `9001` |
| `IsUIPortSeparate` | Whether the administration console and the product instance traffic use separate ports | `No` |

> After changing the web management console port, the **Server URL** setting must also be updated to reflect the new address. Otherwise managed products and endpoints will continue to contact the previous address and will stop reporting in.

---

> Always back up your registry before making changes. Incorrect registry modifications can cause service instability. If the service does not start after the change, import the exported registry key and restart the service.
>
> This procedure applies to Windows installations only. On Red Hat Enterprise Linux and Ubuntu, the port is set in `/etc/opt/mocm/port-config.properties` and applied with the `nginx-port-change.sh` script.

> If **Further Assistance** is required, please proceed to log a [support case or chat with one of our support engineers](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/cm/llms.txt)
