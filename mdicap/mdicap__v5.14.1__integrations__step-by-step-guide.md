<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/integrations/step-by-step-guide -->

# Step-by-step guide

1. Open the Symantec Blue Coat ProxySG management console using a web browser (default URL: http://<bluecoat proxy IP>:8082/)
2. When prompted, enter your user name and password and click "Ok".
3. In the Blue Coat management console, click on the "Configure" tab)

4. On the "Configuration" page, click on the "Advanced configuration" button

5. In the management console menu, go to Policy -> Visual Policy Manager.

6. Click "Launch" to start the Visual Policy Manager.

7. In the Visual Policy Manager, click on the tab where you set the ICAP rule you plan to add file type filtering on.

Info

- In these instructions, the ICAP layer is named "Metascan ICAP RespMod". The tab name on your installation might be different.

The window you see should look similar to the screenshot below.

8. Right click the "Destination" cell of the ICAP rule (line where the "Action" is set to your ICAP service) and click "Set".

9. In the "Set Destination Object", select "New" and click "Apparent Data Type".

10. In the "Add Apparent Data Type Object" window, change the "Name" value to whatever you want (optional) and select the file types you want forwarded to the ICAP server.

11. Click "Ok" twice to get back to the Visual Policy Manager.
12. In the "Visual Policy Manager" window, click "Install policy" to apply the new configuration.
