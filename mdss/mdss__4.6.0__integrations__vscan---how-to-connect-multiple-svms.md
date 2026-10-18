<!-- source: https://www.opswat.com/docs/mdss/4.6.0/integrations/vscan---how-to-connect-multiple-svms -->

# Vscan | How to connect multiple SVMs

When Vscan is enabled, **multiple SVMs** can be connected to the same MDSS instance.

### Step 1: Add the SVM on ONTAP AV Connector

1. From MDSS machine, open the **Configure ONTAP LIFs** app provided by NetApp and available with the ONTAP AV Connector installation.
2. Add the additional SVMs (can be either data LIF or management LIF). In our example, we have used Data LIF as does not require authentication

![](https://uploads.developerhub.io/prod/k8zL/f28q3qcjsg91muwjewbyllp5nlvelww66faahizk7jumxj46rpp69d4gov9604js.png)

3. Once all the SVMs are added, save and quit.

### Step 2: Add each SVM as a different storage unit in MDSS

1. Navigate to MetaDefender Storage Security UI
2. Go to **Inventory** > **Add New** > **Account** and choose **NetApp**
3. For the Account, input:
   1. name
   2. username and password of the privileged user configured on ONTAP
   3. Host (IP) of the SVM
4. For the Storage, input:
   1. name
   2. Share Path. In case you want to add all the SMB shares created under the SVM, input **ONTAP_ADMIN$** (privileged path created by ONTAP) that is available only for the privileged user.
5. Here is an example of how the form should look like

![](https://uploads.developerhub.io/prod/k8zL/qzgm690ua32c3uz28xev25fcc2za3h3ehfyha1s11yde82zifmja1by9lwbj7xs0.png)

6. Click Continue and wait for the storage to be added.
7. If **OPSWAT ONTAP Connector** is installed, do not download or install it.
8. Repeat the steps with all the SVMs you want to add

### Step 3: Add each SVM in the OPSWAT ONTAP Connector config file

1. From MDSS machine, navigate to **C:\ProgramData\OPSWAT-ONTAP-Connector**
2. Open **config.ini** file
3. Set **Storage Units** to the number of SVMs you have added in MDSS
4. Add each Storage Unit and its corresponding details.
   1. **ClientId** can be copied from MDSS UI by Navigating to Storage Units -> Your storage unit card and click the copy button

![](https://uploads.developerhub.io/prod/k8zL/lc01tyxe8sat36qte5lrgmnanpa6xh7frankoscpxtjs2lbqqj5kwwmv7z1gc038.png)

5. Here is an example of how the config file should look like:

![](https://uploads.developerhub.io/prod/k8zL/3n4gvcp4wjnhqqcvys2j6bmqa5cdizsv7l0s8i4p3af7vluwt6eaf9ux2h9wti1s.png)

### **Step 4: Restart OPSWAT ONTAP Connector service**

This service needs to be restarted for the changes to take effect

![](https://uploads.developerhub.io/prod/k8zL/503qqw7adkbt02i7v5v3t31towgyb7lfzf9tsnx3czzb312xsqhvdq3zakhf70ry.png)

### **Step 5: Enable RTP with Event-Based**

One last step is to enable Real Time scan with Event-Based for all the storage units corresponding to your SVMs, so that MDSS can processed the new files

![](https://uploads.developerhub.io/prod/k8zL/1soaq16qpfduy1e33nb2qb4jgqh0ergdw0d0smpf6ob4whe7m2halcc0t3o08ok2.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
