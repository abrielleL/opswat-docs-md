<!-- source: https://www.opswat.com/docs/mdicap/integrations/ara-jaguar-5000 -->

# ARA JAGUAR 5000

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [Configuration via Web-based manager](/docs/mdicap/integrations/ara-jaguar-5000#configuration-via-web-based-manager)

1. In your browser log into Jaguar's Web Administration
2. Go to the **Configuration** page
3. From the menu on the left, click on **Others** under the **Protocol** group
4. From the top menu, select **ICAP**
5. Make sure that **Send Client Address** checkbox is checked
6. Apply changes

images/download/attachments/4864665/jaguar5k_webadmin.PNG

7. Click on the **ICAP Profile** button on the bottom of the page
8. Add a new profile
9. Type in "icap://<IP>:<PORT>/OMSScanReq-AV" to **Vectoring Point 1**
10. Type in "icap://<IP>:<PORT>/OMSScanResp-AV " to **Vectoring Point 3**
11. Apply changes

images/download/attachments/4864665/jaguar5k_webadmin_2.PNG](<https://onlinehelp.opswat.com/icap/images/download/attachments/4864665/jaguar5k_webadmin_2.PNG>) | ![images/download/attachments/4864665/jaguar5k_webadmin_3.PNG

## [Scanning HTTPS Content](/docs/mdicap/integrations/ara-jaguar-5000#scanning-https-content)

1. Go to the Configuration page
2. From the menu on the left, select SSL under the Protocol group
3. Check the Enable SSL checkbox
4. Check the Support SSL intercepting checkbox
5. Upload root certificate
6. Upload root key
7. Apply changes and restart the device

images/download/attachments/4864665/jaguar5k_webadmin_4.PNG
