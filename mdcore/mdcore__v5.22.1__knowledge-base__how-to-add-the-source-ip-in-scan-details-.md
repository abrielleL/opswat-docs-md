<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-add-the-source-ip-in-scan-details- -->

# How to add the source IP in scan details?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Overview**:

By default, when triggering scan from client through a load balancer or proxy server, MetaDefender Core’s Nginx web server will not identify the original client source (but the load balancer or proxy server’s address instead).

This article provides step-by-step instructions to configure MD Core's Nginx web server to display the true source IP address in the scan details.

**Instructions**:

Step 1: Create or Modify the extra.conf File

1. Access the configuration folder:

- **Windows**: Navigate to the directory where MD Core is installed, typically found at: *C:\Program Files\OPSWAT\MetaDefender Core\nginx*
- **Linux**: Navigate to the configuration directory: */etc/ometascan/nginx.d/*

2. Create or Edit the extra.conf file:
3. Add Configuration for Real IP Handling:

- Insert the following lines into the extra.conf file:

set_real_ ip_from 192.168.1.1;

real_ip_header X-Forwarded-For;

real_ip_recursive on;

- **Important**: Replace 192.168.1.1 with the actual IP address of your Load Balancer or proxy server.
- These settings instruct the Nginx web server used by MD Core to trace back and record the original client IP from the X-Forwarded-For HTTP header, which is commonly used by Load Balancers and proxies to pass along the client’s real IP.

Step 2: Restart the OPSWAT MetaDefender Core Service

1. Restart the Service:

**Windows**:

- Open the Services management console by typing services.msc in the Run dialog (Win + R).
- Locate and select the **OPSWAT MetaDefender Core** service.
- Click **Restart**.

**Linux**:

Use the following command to restart the service:

*sudo systemctl restart ometascan*

2. Verify the Configuration:

- After restarting the service, initiate a scan through the Load Balancer or proxy server.
- Check the scan details in the MD Core interface to confirm that the "Source" IP address now reflects the true IP of the client that initiated the scan.

**Troubleshooting**:

- **Configuration Not Taking Effect**: Double-check the extra.conf file for typos, particularly in the IP address and Nginx directives.
- **Service Restart Issues**: Ensure you have the necessary permissions to restart services on the server. If problems persist, consult the logs for errors related to Nginx or MD Core.

**Conclusion**:

By following these steps, you can successfully configure MD Core to display the original client’s IP address in scan details, even when behind a Load Balancer or proxy server. This configuration enhances the accuracy of your logging and provides better visibility into the true source of scan requests.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
