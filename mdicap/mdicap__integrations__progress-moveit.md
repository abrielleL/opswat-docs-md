<!-- source: https://www.opswat.com/docs/mdicap/integrations/progress-moveit -->

# Progress MOVEit

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Progress (former Ipswitch) MOVEit is a Managed File Transfer solution that allows a very simple integration with MetaDefender ICAP leveraging the Multiscanning technology.

Please note Deep CDR and Proactive DLP are not supported currently!

In order to integrate Progress (former Ipswitch) MOVEit with the MetaDefender ICAP please follow the below steps:

1. Login as administrator and go to “Settings”

2. Scroll down to “System” and select “Anti-virus/DLP” from the Content Scanning” section:

3. Add the details of the MetaDefender ICAP as per below:

4. Save by selecting “Change content scanning” and then “Test Content Scanning” (make sure “Scan uploads” is selected)

This will push the EICAR sample to test detection as you can see below:

The setup is now complete. You can test the integration by uploading the EICAR sample which will get blocked as shown below:
