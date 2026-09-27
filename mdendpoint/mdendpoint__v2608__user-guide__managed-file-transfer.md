<!-- source: https://www.opswat.com/docs/mdendpoint/v2608/user-guide/managed-file-transfer -->

# How to use the Managed File Transfer feature?

## What's this feature about?

With the Managed File Transfer feature, MetaDefender Endpoint helps you automate your file transfers and provides advanced security. This feature offers a secure file transfer workflow on critical networks and has streamlined the user experience in document management, making the process of accessing and downloading scanned files seamless and efficient.

## User guide for administrators

### Enable the feature

The Managed File Transfer needs to be enabled beforehand by administrator for users to access and use on endpoints. To do this, administrators can log in to the [console management system](https://gears-beta.opswat.com/) and either enable/disable the feature from Global Setting *OR* Device Groups Setting following the steps below:

- **Global Setting:** Navigate to the *Global* tab under the *Setting* section and check the box that says *Enable MetaDefender Managed File Transfer integration.*

![](https://uploads.developerhub.io/prod/2x2P/7b3ahoyte92dz9bt4hkcukeeuyj5mkll71c2nld1jq5dq3ihluei615ijjhlfjvs.png)

- **Device Groups Setting:** Navigate to the *Device Groups* tab under the Inventory section and check the box that says *Enable MetaDefender Managed File Transfer integration.*

![](https://uploads.developerhub.io/prod/2x2P/21ldz3y7n0llmdatme2whwioc3fsmdoy0i1l1d3jx2rjgqf7ni0bp5awz0sh73gr.png)

Once the feature is enabled via the console management by administrators, users can start uploading or downloading files through the Managed File Transfer feature at ease. __

### Enable uploading files feature

Furthermore, to allow users to upload files from their peripheral and removable media devices, administrators can also manage and enable this via [console management](https://gears-beta.opswat.com/) under *Policies* setting.

![](https://uploads.developerhub.io/prod/2x2P/j7amchjlsh8bz79asb53ip8e40zhv8jwme0z579q0ji78ovgbs3qkg5fnxz9o076.png)

### Disable the feature

To disable the feature, administrators can follow the same steps in console management to uncheck the box for disablement.

### Create a guest user account for transferring files with third parties

To enable seamless and secure file transfer with third parties, administrators can create new guest user using Managed File Transfer server page and set the expiration date for the user. To do so, simply follow these steps:

**Step 1:** Log in to [https://files.opswat.com](https://files.opswat.com/)

![](https://uploads.developerhub.io/prod/2x2P/vgjkqk6e4z2ugieqzxu96lrgjxnrinb867nla74p79p68c7lkhitsid0gyzhngjp.png)

**Step 2:** After login, go to *Users* -> *Guests* and *Create a Guest User*

![](https://uploads.developerhub.io/prod/2x2P/i9nrs5kky5q239j2dnmona2su4iwu3o1z0slj3mr4pr1zvgwu9zysdqad99m4ibs.png)

**Step 3:** Create a new Guest User and set expiration date for the user, then copy its Generated Guest ID. Click *Create*

![](https://uploads.developerhub.io/prod/2x2P/yncy96qourf4vdb0nkk5uv0tkwzcrdmfrmyfzv8zzihu1cu8lmur6ho891jpq1to.png)

![](https://uploads.developerhub.io/prod/2x2P/3xdqam0e586az64cnv2nyjb59eh64s47ngim7b3vw01fd1uoyfp8cz7dzv7yw2gh.png)

**Step 4:** Users can now log in using the copied Guest ID. Simply paste the copied ID to the Enter Identifier field

![](https://uploads.developerhub.io/prod/2x2P/97sq7m0xfr4xxifvzw97jwx9cvcy0xpo1xvcz948dnhnd2m5efwepzsnxnfm50gf.png)

## User guide for end users

### Upload files from peripheral and removable media to Managed File Transfer

Users can upload files from peripheral and removable media such as USB drives to the Managed File Transfer. To do so, simply follow the steps below:

**Step 1:** Navigate to the Peripheral Media Protection feature on MetaDefender Endpoint. Choose the media that you wish to copy data from.

![](https://uploads.developerhub.io/prod/2x2P/taiox6pztyh9lqe4ujr4ucf3k0ska56cril86tdtpi9ymg7zkjxwubj0p4v4b3ic.png)

**Step 2:** Choose file or folder to copy from media to local drive.

![](https://uploads.developerhub.io/prod/2x2P/ywqwqj0ssdlmcj78xnx6l87jvaboakx6s37m9yrx5l0knfk86vs8g7pgtndnut14.png)

**Step 3:** Wait for the process to be completed. If the feature of uploading files to Managed File Transfer is enabled, the files will be automatically uploaded to Managed File Transfer. This means that files will be both copied to local drives and uploaded to Managed File Transfer at the same time, ensuring seamless file transfer with no interruption or hiccups.

![](https://uploads.developerhub.io/prod/2x2P/u5uyjgnm09ghamg7grx3kk9rei969hsihh9yjx9xtngoia7w4xtdgcbh5geaurdw.png)

**Step 4:** Once uploaded, MetaDefender Endpoint will send a pop-up notification to announce the completion of the process and provide the Guest ID, which is required in accessing and downloading files. Guest ID is also viewable to administrators on the Managed File Transfer server.

![](https://uploads.developerhub.io/prod/2x2P/9y1atx0uysr7hhv6ykxjf3wp0wlynwl6xjbnsw8t26hza8veg1eah2sljbfjx8nr.png)

### Upload files to Managed File Transfer server using Guest ID

Users can upload files directly to the Managed File Transfer server. To do so, simply follow the following steps:

**Step 1:** Log in to [https://files.opswat.com](https://files.opswat.com/) .

![](https://uploads.developerhub.io/prod/2x2P/vgjkqk6e4z2ugieqzxu96lrgjxnrinb867nla74p79p68c7lkhitsid0gyzhngjp.png)

**Step 2:** Users can now log in using the copied Guest ID. Simply paste the copied ID to the Enter Identifier field

![](https://uploads.developerhub.io/prod/2x2P/97sq7m0xfr4xxifvzw97jwx9cvcy0xpo1xvcz948dnhnd2m5efwepzsnxnfm50gf.png)

**Step 3:** Once logged in, click *Upload Files* and choose files or folder to upload

![](https://uploads.developerhub.io/prod/2x2P/b3g91xipojpiomu3445po0fefj5x3cx15jjomrj1n4wp5qu5lturdgjtimvbohm7.png)

### Download allowed files from Managed File Transfer

Once the files are uploaded to the Managed File Transfer, users can view and access them using details such as Guest ID and Server URL provided by admins or file uploaders.

> **NOTE**
>
> While all uploaded files are viewable on Managed File Transfer, only allowed files can be downloaded by the users.

To download allowed files, simply follow the steps below:

**Step 1:** Users need to collect the Guest ID and Server URL to be able to access the folder. These details are managed by administrators and can be provided using the Managed File Transfer server.

![](https://uploads.developerhub.io/prod/2x2P/n5og0xkoqrr8nkq8ep3m6cvit9r473ei3pcmpztm0xq3b5qd4w2k2uzwgqfoc0pd.png)

**Step 2:** Enter the Guest ID and the Server URL.

![](https://uploads.developerhub.io/prod/2x2P/ptfctpod2xvaxkra0fs23wzzdeua0bswuhzm781skjhyrizyw9o75xcpskdqezci.png)

**Step 3:** Once the process is complete, users can view the files right at the MetaDefender Endpoint user interface. Simply click the + button to collapse and view the full file list.

![](https://uploads.developerhub.io/prod/2x2P/hosuq5za4pv7gfacbvw98639q5q5g95lev7lc4j3rofikjrretxjr4n50mnvyd7j.png)

**Step 4:** Choose the file you wish to download and click *Download*.

![](https://uploads.developerhub.io/prod/2x2P/b5qmeto0vj38grh9g6acadbipqbcerd35nzxevxp4xx5jtb9yfhxfr7nmcha0b1g.png)

**Step 5:** Once the download is completed, users can choose *Show In Folder* to access the files.

![](https://uploads.developerhub.io/prod/2x2P/mrebiqpoewh068fcahjfzq5uto4by93ksejx8ara1vm9iba08mz44ook7o7nemlm.png)

![](https://uploads.developerhub.io/prod/2x2P/p4nokq2u6gyuos40sk7imk71zshtngt27quyfbz3ct2gkfm4v57qbunms4tn7g8w.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdendpoint/llms.txt)
