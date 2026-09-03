<!-- source: https://www.opswat.com/docs/cm/product-management/metadefender-kiosk -->

# Enroll MetaDefender Kiosk

Enrolling MetaDefender Kiosk instances into My OPSWAT Central Management centralizes your oversight and standardizes security controls across your infrastructure.

You can enroll a Kiosk instance **during** or **post-installation** via the Kiosk Management Console.

Note After enrollment, configuration settings on the local Kiosk will be grayed out, as management is now centralized within My OPSWAT Central Management console.

## MetaDefender Kiosk Management Console [Post-Installation]

Use this method for Kiosk instances that are already installed and running.

### **Step 1: Retrieve Enrollment Details**

To enroll a new Kiosk instance, the **Server URL** and **Registration Code** must first be obtained from My OPSWAT Central Management Console:

- Access My OPSWAT Central Management console.
- Select the **+Enroll Product** button on the left menu.
- Choose **MetaDefender Kiosk** from the list of available products.
- In the prompt that appears, select the appropriate operating system (Windows or Linux).
- Copy the provided **Server URL** and **Registration Code**.

![](https://uploads.developerhub.io/prod/97qW/l7jckattysydgb2p0wu9q77jrxurv23ewbwsbgta3951x6gkkcgwh8ocv574w27l.png)

### **Step 2: Enroll MetaDefender Kiosk Instance**

With the Server URL and Registration Code ready, the enrollment is finalized within the MetaDefender Kiosk Management Console:

- Log in to **MetaDefender Kiosk Management Console**.
- Select the **Unmanaged** button in the top-right corner.
- Enter the **Server URL** and **Registration Code** from Step 1.
- Select **Enroll Now**.

![](https://uploads.developerhub.io/prod/97qW/5vdpf1lzedqy3t5vrpk58axsuy2bhab1hmka8fukv5lk2uatz96umxmi67djtwiv.png)

### **Step 3: Verify Kiosk Enrollment**

Once connected, the Kiosk status will change to "**Product is Managed**”.

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.

![](https://uploads.developerhub.io/prod/97qW/p3oxhx8lwcq7v8jwo5jryve9dihkwviqrhlr3nyurnjtjfu9yphlqnzl59yy30cf.png)

## Kiosk OOBE Setup Wizard [During Installation]

The MetaDefender Kiosk Out-of-box Experience (OOBE) Setup Wizard allows for immediate enrollment during initial configuration.

- Navigate to the enrollment step within the OOBE Setup Wizard.
- Input the **Registration Code** and **Server URL**. Refer to [Step 1: Retrieve Enrollment Details](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-1-retrieve-enrollment-details) for guidance.
- Select **Enroll** to finalize the connection.

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.

![](https://uploads.developerhub.io/prod/97qW/gh2gt1ofbe402dha9hd7mnjrvnrowzexfrnrdpvwwfz21uwxys0y7e8nh2adz99s.png)

## Kiosk Setup Wizard [During Installation]

The MetaDefender Kiosk Setup Wizard offers immediate enrollment into My OPSWAT Central Management during installation.

- Navigate to the enrollment step within the Setup Wizard.
- Input the **Registration Code** and **Server URL**. Refer to [Step 1: Retrieve Enrollment Details](https://www.opswat.com/docs/cm/product-management/metadefender-kiosk#step-1-retrieve-enrollment-details) for guidance.
- Select **Enroll** to finalize.

![](https://uploads.developerhub.io/prod/97qW/i0tu3awlpetlcibsqvln9qc1mm4ld307j6k2nzfus5c24ze4uzozw1xl2va2sok1.png)

Once installation is complete, navigate to **Inventory > Devices** in My OPSWAT Central Management console to verify that the instance is active.
