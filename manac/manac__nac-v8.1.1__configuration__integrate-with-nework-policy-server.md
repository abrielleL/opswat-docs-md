<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/configuration/integrate-with-nework-policy-server -->

# Integrate with Nework Policy Server in Proxy mode

First we have to register Network Policy Server in Active Directory to allow authentication based on user accounts we created in domain.

**To authorize NPS in AD:**

- Logon to server with NPS using account with domain admin credentials.
- Go to **Start / Administrative Tools** and then click **Network Policy Server**.
- Right-click on **NPS (Local)** and from context menu click **Register server in Active Directory**.

---

Now it’s time to inform NPS about our NAC and establish shared secrets as form of identification when NAC will be requesting authentication and authorization from RADIUS and Active Directory.

**To add NAC as RADIUS client:**

- Logon to server with NPS using account with admin credentials.
- Go to **Start / Administrative Tools** and then click **Network Policy Server**.
- Expand **RADIUS Client and Servers**.
- Right-click on **RADIUS Clients** and click **New** from context menu.
- In **New RADIUS Client** window **Settings** tab enter:
- **Friendly name of the NAC** – name to recognize router, usually same as hostname.
- **Address (IP and DNS)** – IP address of the router or hostname – if hostname used proper hostname needs to be registered in DNS prior to RADIUS configuration.
- **Shared secret** – passphrase which was configured on router which will allow to identify NAC.

Config 802.1x for Wired and Wireless connection

- Go to **Start / Administrative Tools** and then click **Network Policy Server**.
- Click on **NPS(Local)**
- On the Right panel, choose **RADIUS server for 802.1X Wireless or Wired Connection** from context menu.
- Click on **Configure 802.1X**

Follow these steps for complete the wizard - Setup Network Policy for Secure Wired Connection

Check policy for secure wired connection we have just create

### [Troubleshooting](/docs/manac/nac-v8.1.1/configuration/integrate-with-nework-policy-server#troubleshooting)

Troubleshooting with NPS is quite difficult due to the lack of information in any case, if you want to analyze NPS log, open “event viewer” and select “Network policy and access services”. Below an example:
