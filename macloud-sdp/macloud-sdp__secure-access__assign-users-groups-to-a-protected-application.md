<!-- source: https://www.opswat.com/docs/macloud-sdp/secure-access/assign-users-groups-to-a-protected-application -->

# Assign users groups to a protected application

Objective: Protect an application using the Hosted SDP Gateway; no SAML integration, leveraging a local user.

1. Example application that is locked down to only accept traffic from a Hosted SDP Gateway: <http://demo.cloud.impulse.com/> (firewall on the application server only accepts traffic from the Hosted Gateway)
2. The Hosted Gateway is an additional purchase. **You will need to get it enabled to continue.**Review the details on product bundling/packaging here to understand what is included or not in the standard MetaAcess: <https://www.opswat.com/uploads/assets/files/Product-Guide_compressed-1.pdf>
3. After upgrading, enable the Hosed Gateway.
4. Create the protected application, pointing at the demo app: [demo.cloud.impulse.com](http://demo.cloud.impulse.com) . You will need to **Enable Secure Access**, first, within **Secure Access > Protected Apps**. Click **Add Protected App**, then choose **SDP Method**. Fill in the following information:

| **Field** | **Value** |
| --- | --- |
| *Application Name* | Demo |
| *Access Mode* | Monitor |
| *Application Type* | Web Application |
| *Application URL* | <http://demo.sdp.opswat.com> |
| *Ports* | 80 TCP |

5. Select **Save & Next**.

6. Select an End User, then click **Assign**.

7. Download the MetaDefender Endpoint from your MetaDefender IT-OT Access console for the client device.

8. Choose the Persistent MetaDefender Endpoint. Note: SDP is **not** always installed at the time MetaDefender Endpoint is. You will only see it in the Tray if you have added the endpoint device to a group that has SDP enabled or if SDP is enabled globally.

9. After enabling, SDP will auto-install, and appear in the tray. Click **Sign In**.

10. Login as the end user. You should see your Demo app entry.

11. Access the Demo app.
