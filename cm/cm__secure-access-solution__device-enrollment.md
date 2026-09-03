<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/device-enrollment -->

# Device Enrollment

## Introduction

The Device Enrollment feature allows administrators to easily import devices into the system. Each device will be automatically assigned to the appropriate Access Profile based on the provided information. Using a straightforward import mechanism, administrators can upload an Excel file with device details, including MAC addresses, device types, and operating systems.

This feature is designed for non-802.1X capable devices, including IoT.

## Configuration

1. **Configure Rule to handle IoT Devices**
   - Navigate to RADIUS NAC --> Rules
   - Create Rule with the following information

![](https://uploads.developerhub.io/prod/97qW/hmk8x6mo2khetkjfpd754pmeakm4jaxfez4lq32sywvugc9hx1uds4wd4s7hyv8o.png)

The above Rule will assign a `IoT`_Unknow_Server`` access profile to Device(s) that match with all of conditions defined.

## Enroll Device

### For Devices that do not yet exist on My OPSWAT Central Management

1. **Importing Device List**
   - From the console UI of **My OPSWAT Central Management,** navigate to **Inventory** -> **Devices**
   - Click on the **Import** button, then click **Download** **Template** **file**

![](https://uploads.developerhub.io/prod/97qW/vzto7v4e6w6oyycun2fx6z5o7uhs1y73p3rlmv125uw5i84t32j6gtm8wy9lfg21.png)

- Open the template spreadsheet that was downloaded and add a **Device MAC Address** and **Device Group** Name. Other available optional fields are **Operating System**, **Device Type**.

![](https://uploads.developerhub.io/prod/97qW/t4bupqqga87gbwijuxahzpkytelaea0yt48o2iecwoiujg5zfw6dzz5rf9t9eq31.png)

- Click on Choose File, locate and select the template spreadsheet then click Import.

- After a successful import, the device information should be displayed correctly on the MDITA console.

![](https://uploads.developerhub.io/prod/97qW/86kb9ropvi5yxtpne0z4u29wyt6otmsn36m5mhfp7rb0jhqeufchfzxiezfysn7n.png)

![](https://uploads.developerhub.io/prod/97qW/e7vy5gk2w29exwcg0lnoq7627qpgrxg67asuv2ghunh6nmekhgp8y5km4tghfvjx.png)

- Upon accessing the Network, the Device(s) will be assigned to the appropriate RADIUS Rules defined by the Administrator.

![](https://uploads.developerhub.io/prod/97qW/rm8g2g7tlu6hecfb7zupm38szygw8wm36wb8lypjjqsawc9m7sjz8m7qh9c0ceci.png)

### For Devices already present on My OPSWAT Central Management

1. **Enroll a device**
   - An Unknown Devices already existed on **My OPSWAT Central Management** but without additional information such as **Device Type**, **OS**

![](https://uploads.developerhub.io/prod/97qW/05nz3aay1kl2b7c8kkk79t9touuttxr85ituvyaf7jvroavmf53ij3id6e2duaci.png)

- RADIUS NAC can enforce the Unknown Device by mapping the Device's information with multiple conditions in RADIUS NAC Rules. We will use the same [Device Enrollment Configuration](https://www.opswat.com/docs/cm/secure-access-solution/device-enrollment#configuration)[ ](https://www.opswat.com/docs/cm/manac/nac-cloud/device-enrollment#configuration)for this scenario.

- On the template spreadsheet, fill in additional information for the Device

![](https://uploads.developerhub.io/prod/97qW/90d66oeojauukdr09wydthu4al6us4otwprckzptzlueln0uu7ic0fs6rfd4ka4q.png)

- After import successfully, the Enroll information should display correct

![](https://uploads.developerhub.io/prod/97qW/8tb1mna7iudhshzo0d267ksmvl9g2q2k3ndowkn9hove5loiu38b20rm406d5bei.png)

- Upon accessing the Network, the Device(s) will be assigned to the appropriate RADIUS Rules defined by the Administrator.

![](https://uploads.developerhub.io/prod/97qW/ijxv5vrl3nsgcg5t3erdo7fczb831jfvk425u0kzfmbg509h6i0s44hpizp8avrp.png)

## Troubleshooting

For any issues during the enrollment process, please refer to the details at [Device Enrollment FAQ](https://www.opswat.com/docs/cm/secure-access-solution/device-enrollment-faq).
