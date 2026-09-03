<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-do-i-get--failed-to-create-server-shutdown-socket--when-inst -->

# Why do I get "Failed to create server shutdown socket" when installing OCM 10 on-prem?

**Issue:** While installing OCM 10 on-prem on Windows OS, you may encounter the following error message:

*Failed to create server shutdown socket on address [localhost] and port [8005] (base port [8005] and offset [0])*

*java.net.BindException: Address already in use: bind*

**Cause:** This error occurs because the default Tomcat port (8005) is already in use by another process on the system. Tomcat requires a unique port for its shutdown socket, and a conflict prevents the service from starting.

**Resolution:**

- Open the Tomcat configuration file:

*D:\Program Files\OPSWAT\MOCM\tomcat\conf\server.xml*

- Change the port number to an unused port (for example, 8006)
- Save the file and restart the OCM service.

> **Support:**
>
> If Further Assistance is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).
