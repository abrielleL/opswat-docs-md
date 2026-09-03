<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/private-gateway-test-application -->

# Private Gateway Test Application

This section guides you how to set up an application that can be only reached via a private gateway SDP and demonstrates a user experience.

In this article you will learn how to:

- Enable the testing web app that ships with the SDP Private Gateway.
- Define the Private Gateway test app as a protected application in SDP.

Before you start this guideline, you must install a private gateway and connect it to your account. If you have not done so, you can follow guidelines in [Set Up Gateways](https://www.opswat.com/docs/cm/secure-access-solution/set-up-gateways)

To simplify testing private gateway connectivity we ship with a test resource located on the same VM.

When this feature is enabled a web application is available at [http://172.18.0.200](http://172.18.0.200/). This should be added as a protected application in the MA UI. The port is the default HTTP port 80/TCP. The only action to take is to enable or disable it. Further configuration (IP address, port) is possible in the future.

1. From the private gateway configuration tool, enable the test application by navigating to **[F11] Test App** and selecting **Enable**.
2. Navigate to your MetaDefender IT-OT Access console to add this application. *Note: Enable secure access first if needed.*
3. Select **SDP Method** as the method to protect this application.
4. Add the test app:
   1. Select **Web Application** as the Application Type
   2. Enter [http://172.18.0.200](http://172.18.0.200/) as Application URL, the system will auto-fill in the port 80/TCP for you.
   3. Access Mode: Monitor for testing purpose. You can set this to “Enforce” to ensure that the device must be met with [Access Rules](https://www.opswat.com/docs/cm/secure-access-solution/access-rules) before being allowed access to the application.
5. Add any users or groups to have access to this resource. You can refer to [Provision Users](https://www.opswat.com/docs/cm/secure-access-solution/provision-users) to understand how to invite an end-user or import user groups from your IdP.
6. Add any gateways to have access to this test resource.
7. Verify that SDP is enabled either globally (**Settings > Global > Device Agents**) or at a device group level (**Inventory > Device Groups >** select group **> Settings**).
8. It will take sometime for MetaDefender Endpoint retrieve settings from **MetaDefender IT-OT Access** to enable SDP. After it enables SDP successfully, you can login on the tray menu.
9. Click Log in to launch the MetaDefender Endpoint UI and sign in with the user you assigned to the testing app. Follow guidelines from the MetaDefender Endpoint UI to log into SDP.
10. After a user authenticates successful, the user will see applications the user can access based on user permission and access rules. From now on, the user can access applications/resources as normal they do
11. Now on the test device, you can access to the testing app hosted on the private gateway through your browser [http://172.18.0.200](http://172.18.0.200/) or click on the app on the SDP user interface.
