<!-- source: https://www.opswat.com/docs/mdicap/integrations/bypassing-metadefender-icap-server-temporarily -->

# Bypassing MetaDefender ICAP Server temporarily

This guide describes how to enable and disable ICAP server on Symantec Blue Coat ProxySG.

Warning

This documentation is assuming that MetaDefender ICAP Server is already configured and working properly.

## [Enable MetaDefender ICAP Server](/docs/mdicap/integrations/bypassing-metadefender-icap-server-temporarily#enable-metadefender-icap-server)

To enable MetaDefender ICAP Server on Blue Coat:

1. Open the Blue Coat Management Console.
2. Go to "Configure" tab > "Advanced configuration" button.
3. In the left side menu, go to "Policy" > "Visual Policy Manager"
4. Click "Launch"
5. In the VPM window, right click on the service you want to enable tab (typically "ICAP Respmod" or "ICAP Reqmod")
6. Click "Enable layer".

   - The tab color should turn black.
7. Click "Install policy

## [Disable MetaDefender ICAP Server](/docs/mdicap/integrations/bypassing-metadefender-icap-server-temporarily#disable-metadefender-icap-server)

To disable ICAP server on Blue Coat:

1. Open the Blue Coat Management Console.
2. Go to "Configure" tab > "Advanced configuration" button.
3. In the left side menu, go to "Policy" > "Visual Policy Manager"
4. Click "Launch"
5. In the VPM window, right click on the service you want to disable tab (typically "ICAP Respmod" or "ICAP Reqmod")
6. Click "Disable layer".

   - The tab color should turn red.
7. Click "Install policy"
