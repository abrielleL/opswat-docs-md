<!-- source: https://www.opswat.com/docs/mdendpoint/validation-endpoint/features -->

# Features

### **File Blocking for Removable Drives**

- **Initial Block:** All files on the removable drive are blocked initially, users can’t directly open or copy these files.
- **Drive Access**: Users can still access the drive via Windows Explorer, the drive itself isn’t fully blocked.
- **Admin Configuration**: Administrators can configure a policy to allow copying files from USB to the local filesystem without scanning or accepting files.

### **On-Access Validation**

- **Validation:** Validate files automatically with the manifest file evaluated from the Kiosk as they are accessed or opened by users or other programs.
- **Intuitive UX:** Users have the option to work in "Windows Explorer" right-click on a file or folder and select the "unblock" option. This action triggers a validation process for the selected files, subsequently unblocking those that are determined to be allowed by the system.

### **Temporarily change features**

- **Disable** features with/without duration time via the Command Line
- **Enable** features with/without duration time via the Command Line
- **Update** manifest settings commands, Update certificate file and Set the manifest trust days
- **Show** drive information for a specific drive or all
- **Allowed devices:** List, Reset or Add allowed devices

### **BadUSB protection**

- Discover and block USB Drives that masquerade keyboards to infect target computers.
