<!-- source: https://www.opswat.com/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms -->

# Vscan | How to connect multiple SVMs

When Vscan is enabled, **multiple SVMs** can be connected to the same MDSS instance.

### [Step 1: Add the SVM on ONTAP AV Connector](/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms#step-1-add-the-svm-on-ontap-av-connector)

1. From MDSS machine, open the **Configure ONTAP LIFs** app provided by NetApp and available with the ONTAP AV Connector installation.
2. Add the additional SVMs (can be either data LIF or management LIF). In our example, we have used Data LIF as does not require authentication

3. Once all the SVMs are added, save and quit.

### [Step 2: Add each SVM as a different storage unit in MDSS](/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms#step-2-add-each-svm-as-a-different-storage-unit-in-mdss)

1. Navigate to MetaDefender Storage Security UI
2. Go to Storage Units -> Add new storage unit -> Choose NetApp -> Add new Account
3. For the Account, input:

   1. name
   2. username and password of the privileged user configured on ONTAP
   3. Host (IP) of the SVM
4. For the Storage, input:

   1. name
   2. Share Path. In case you want to add all the SMB shares created under the SVM, input **ONTAP_ADMIN$** (privileged path created by ONTAP) that is available only for the privileged user.
5. Here is an example of how the form should look like

6. Click Continue and wait for the storage to be added.
7. If **OPSWAT ONTAP Connector** is installed, do not download or install it.
8. Repeat the steps with all the SVMs you want to add

### [Step 3: Add each SVM in the OPSWAT ONTAP Connector config file](/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms#step-3-add-each-svm-in-the-opswat-ontap-connector-config-file)

1. From MDSS machine, navigate to **C:\ProgramData\OPSWAT-ONTAP-Connector**
2. Open **config.ini** file
3. Set **Storage Units** to the number of SVMs you have added in MDSS
4. Add each Storage Unit and its corresponding details.

   1. **ClientId** can be copied from MDSS UI by Navigating to Storage Units -> Your storage unit card and click the copy button

5. Here is an example of how the config file should look like:

### [**Step 4: Restart OPSWAT ONTAP Connector service**](/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms#step-4-restart-opswat-ontap-connector-service)

This service needs to be restarted for the changes to take effect

### [**Step 5: Enable RTP with Event-Based**](/docs/mdss/4.4.2/integrations/vscan---how-to-connect-multiple-svms#step-5-enable-rtp-with-event-based)

One last step is to enable Real Time scan with Event-Based for all the storage units corresponding to your SVMs, so that MDSS can processed the new files
