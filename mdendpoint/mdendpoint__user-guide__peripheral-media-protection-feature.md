<!-- source: https://www.opswat.com/docs/mdendpoint/user-guide/peripheral-media-protection-feature -->

# How to use Peripheral Media Protection

## Overview

Peripheral Media Protection is one of the key features of MetaDefender Endpoint, designed to safeguard endpoints from USB-borne threats. It scans peripheral and removable devices for potential malware before they are made accessible, blocking any malicious files from accessing endpoint devices and critical environments. This feature provides proactive and comprehensive protection, offering peace of mind by stopping USB-based attacks at the point of entry.

---

## User guide for Administrators

This feature has two different modes that are controlled and set via the administrator management console.

- Full block mode
  - Always block removable media
  - Allow users to do selected actions
- On-Access file scanning

![](https://uploads.developerhub.io/prod/2x2P/wbjdyg6bbmeux8vcsl7b8128cwq3h92zyoh7wh2f1omwnhflb1guh6u07m99230x.png)

To set the mode for the feature, administrators can follow the steps below:

**Step 1:** Log in to the [console management system](https://gears-beta.opswat.com/)

**Step 2:** Choose *Policy Management* > *Policies*. Then click on the policy group you would like to make changes to

![](https://uploads.developerhub.io/prod/2x2P/feovbamhvwhzdobsm5xa471mp7kx61jhhjgjr7ptnt55zzji5id923l4n7myywio.png)

**Step 3:** Choose *Advanced Endpoint Protection* > *Enable Threat Detection for Windows*

![](https://uploads.developerhub.io/prod/2x2P/r6cvm6xjva1q8ymwz7f12jgzvsdvaog8pof1j68m6bqfly64qp5f3gkwynxz4j1p.png)

![](https://uploads.developerhub.io/prod/2x2P/qa1s62cgy8syw47f4zya0rb6q7kzrb0rhwqtm5sqvwytrgdjqg9s0e3jdzucfhx7.png)

**Step 4:** Scroll down to the *Removable Media Protection* tab. Keep scrolling to the section titled *When removable media is connected* , and select the mode to enable in the policy.

![](https://uploads.developerhub.io/prod/2x2P/kb4euhwau9x08ixjehwkmuxzzrdjof7e6hcdxbwjxkwlqtyyr9647hnzzkk2wdws.png)

---

## User guide for end users

### Mode: On-Access file scanning

#### ***Access files from the USB***

To access files from peripheral devices, users can choose to scan selected files that they wish to work on or scan the entire USB. Once the files are found to be clean, users can access the files as usual. To perform a scan, simply follow the steps below:

**Step 1:** Plug in the peripheral device into the endpoint’s port and open MetaDefender Endpoint. Select the Peripheral Media Protection section. Choose the peripheral device you would like to access:

![](https://uploads.developerhub.io/prod/2x2P/jx89k9biethnec8er6w5vihm8oeantyifjpkbhgxs48xanptph8oclakrnalhzs6.png)

**Step 2:** To access files from peripheral devices, users can choose to scan selected files they wish to work on or scan the entire USB.

Choose *Open folder*  to scan selected files or *Unblock* to scan the entire device.

**Case 1: Access selected files**

Through the user interface of MetaDefender Endpoint, clicking *Open folder*, will open Windows Explorer and display the device’s folder.

![](https://uploads.developerhub.io/prod/2x2P/9twmx7eo7syupdrfpjagcqgyj70o1iezysublj875hmpe8df7n65p0et80pizxfm.png)

Choose the file(s) you would like to access.

> **NOTE**
>
> Every file will be scanned before its execution or access.

![](https://uploads.developerhub.io/prod/2x2P/qkix2gt0k6qretbkqj0j2w9fe5hjsg3u8hnehjcofed87fkos71b7l21hn2th1dn.png)

Wait for the scan process to complete:

![](https://uploads.developerhub.io/prod/2x2P/bcw0kffkkcnchrmx5q3f1fscqutoa2vska1iji9iodth5p4f1ahenk7njods37fs.png)

If the file is clean (i.e., no threats detected), user can access the file as usual:

![](https://uploads.developerhub.io/prod/2x2P/i6qdcfwas7iaaiboj7ascgtkeqedrep8d6c9bk6oloagxdhpy4eu0ia8rw9056mp.png)

If the file is deemed a threat, it will be blocked. The status will be reflected in the user interface of the MetaDefender Endpoint for the users’ awareness:

![](https://uploads.developerhub.io/prod/2x2P/oagdndcxlxagk56ec7u4h2596w9aryuhftsd8uc5u0g9okfscl884in8jrz34jke.png)

![](https://uploads.developerhub.io/prod/2x2P/lc8pf1nk5f4eqxtt94dmgqmyqc11a7zuh8egdfy1tuit8f79kac8pawg546qftge.png)

**Case 2:** **Scan the entire device**

Through the user interface of MetaDefender Endpoint, click *Unblock*. This will initiate the scan process.

![](https://uploads.developerhub.io/prod/2x2P/odom8w3m6xmnk4cplk882rglt0yecoqj4rk4kzeywk1qm77ruyi3hzoxwzqp3u45.png)

Wait for the scan process to complete.

![](https://uploads.developerhub.io/prod/2x2P/x5aa5p40ypjygvoaooqr7zasi6o8utitdtd0qxibemmlf56cvk4cmk0qo9h5scdz.png)

When the scan is complete and no threat is found, users can either look at the scan report by clicking *Report,* or continue using the device as-is.

![](https://uploads.developerhub.io/prod/2x2P/l81otpqremuzzdpcay2zi4i8azsn9fz06if4v27me30ijc3tdhsx5hz3b5u9sid9.png)

If a threat is found, the device will be remained blocked. User can view the scan report for more details.

![](https://uploads.developerhub.io/prod/2x2P/v9d6y8m19dk5l5gljoj5b5r94s0bp5jkxy6n5ps7ycebguy74mc8ngigahcjp2qx.png)

#### ***Copy files from the USB***

**Step 1:** Plug in the peripheral device into the endpoint’s port and open MetaDefender Endpoint. Select the Peripheral Media Protection section. Choose the peripheral device you would like to copy files from and click *Open folder.*

![](https://uploads.developerhub.io/prod/2x2P/97rnz11l6utq9quy2pdzyj9ukgt9r9flxiv9fzt99m2j11ik0hg0g057ak005jcz.png)

**Step 2:** Windows Explorer will display, select the file(s) you would like to copy to the local drive, then right click >> *Copy* .

![](https://uploads.developerhub.io/prod/2x2P/jvdvutsqob0a2nhlrybf9b57grl4ppd0xrgr2p8x8jizial8ivydg1z70j1ilwh1.png)

**Step 3:** Choose the destination folder in local drives you would like to copy the file(s) to, then right click >> *Paste.*

![](https://uploads.developerhub.io/prod/2x2P/op8t53spz8wwfyldafdjs3le77u33vyea6ddph998juljueow82j5rbmsr2vwvd9.png)

**Step 4:** The scan process will be triggered, wait for it to complete.

![](https://uploads.developerhub.io/prod/2x2P/rtcf923tbzmmmo17v34en4pavw1ufde9z3mg25ayzm2sp1kiegzlaj5v7yzmvrh6.png)

**Step 5:** Once the scan is complete, clean (allowed) file(s) will be copied to the local drives and accessible to the user.

![](https://uploads.developerhub.io/prod/2x2P/5icyo5s17vndqizk2opbbjtt9woqytkym3n752ggmxcecm20di7v9jyouzi7lks0.png)

---

### Mode: Full block

#### ***Unblock a device***

**Step 1:** Plug in the peripheral device into the endpoint’s port and open MetaDefender Endpoint. Select the Peripheral Media Protection section.

![](https://uploads.developerhub.io/prod/2x2P/1h3ix0jd4cbmkp3jfwrdxh11qcisibefgb0kt7sd683m5xp9cm22ckdf973y0wj5.png)

**Step 2:** Click *Unblock* to start the scan process.

![](https://uploads.developerhub.io/prod/2x2P/t8rojd1gp9uu7j77u2g8nj08z1kl8hmj3r8vc33aykx31v8vysk9bcl4ogy5fzfr.png)

**Step 3:** Wait for the scan process to complete.

![](https://uploads.developerhub.io/prod/2x2P/utv3j6ef4589c4whk7jasyxuy0nkyjmho3seorygdoa14ewnse6d0t59itu6ctxd.png)

**Step 4:**

***Case 1: Unblock successful***

Once the scan is complete and no threat is found, the device is deemed clean and accessible to the user.

![](https://uploads.developerhub.io/prod/2x2P/umr5wpmol939gtoumcwyv5dm0q8nsnjeys68jjzt66d7matv2q5zb8uipxkk2s31.png)

A pop-up notification will display in the bottom right corner of the screen, indicating that the peripheral media device is now accessible.

![](https://uploads.developerhub.io/prod/2x2P/e3gp7nk1139jpmx36g6hldtkg9dujza2y3a7w38g1xakxgf9krtz2wotp5v900ik.png)

***Case 2: Unblock failed***

After scanning, if the media contains malicious content, it is blocked and users will NOT be able to access the media device or its contents.

![](https://uploads.developerhub.io/prod/2x2P/w363et5hdodhrqmkfp7p5yc3aavpk8w4amjllr6to5b3mvg7itrpvkxmxq5mousg.png)

Simultaneously, a pop-up notification will also show at the bottom right corner of the screen, indicating the status of the scan.

![](https://uploads.developerhub.io/prod/2x2P/v8a2f2sa0x0oo5morogysqewqultysyxhl9qqerp1g7j5tapb2qb2h2e2nay5rhf.png)

A scan report with details of blocked files, potentially vulnerable files, etc. will display for users to have more information on the device.

![](https://uploads.developerhub.io/prod/2x2P/w0x3ugk89uky68snwys9evoa7ktq8qgyj3g93tq0upsh3dapqiyu3u56mhissmmd.png)

**Step 5:** If the device is safe and accessible, to access the folder or the files in the device, users can click *Open folder to access files* directly from the interface of MetaDefender Endpoint or from native applications (Windows Explorer, Word, Excel, etc...).

![](https://uploads.developerhub.io/prod/2x2P/fqhq5ecthdok384nng1fvdvev74xrsom11oue8rtdun11nwcm2r3y5j62792tz2o.png)

![](https://uploads.developerhub.io/prod/2x2P/rysvh7hdrlimf7lhuznc9g5hpajzbo7801x73913dzb86411kyuij4t0rzpemv02.png)

**Step 6:** Users can access the scan report by clicking the *Report* button

![](https://uploads.developerhub.io/prod/2x2P/5e5zog6c828kyho8ilhfe3tg6edufu6rvwrxbezg7u7cerpmimkvvz13wgtcj2hf.png)

#### ***Copy files from the USB***

**Step 1:** Plug in the peripheral device into the endpoint’s port and open MetaDefender Endpoint. Select the Peripheral Media Protection section. Choose the peripheral device you would like to copy files from and click *Copy from.*

![](https://uploads.developerhub.io/prod/2x2P/cqd4u7irt1dl4ls9cicabxy1j1jzrti9bfrood6tkr3j3u5w9eea2d9jt8ynkmbk.png)

**Step 2:** Click on the + icon to expand the view of folders and files of the peripheral media device.

![](https://uploads.developerhub.io/prod/2x2P/q5oqnmwf0aiqe0kf08qubj1igyh72nx37u1cd8elu406g3dy3bzwi73q1jdw56zi.png)

**Step 3:** Select files or folders to copy from the media to the local drive. Then click *Next.*

![](https://uploads.developerhub.io/prod/2x2P/rglx7yqr50ushgwqphges6cp9348rmadin74sqn1ayl0lk7xcov4jln5bickr7z9.png)

**Step 4:** Click *Copy.*

![](https://uploads.developerhub.io/prod/2x2P/4pni8gqkh6n4d62b6qy9b7bslnpng0p3z4qgwo07q2m26ojsmf2wmwxyt732qhii.png)

**Step 5:** By clicking *Copy,* MetaDefender Endpoint triggers the scan process, to ensure the file or folder are safe before copying.

![](https://uploads.developerhub.io/prod/2x2P/ueuk2ty6d9eu5r3isc94r6eyg73cuqu3yztbvpsyax6h5p9x30mbe1hxerxwfmrv.png)

**Step 6:** Once the scan is complete, any file/folder that is safe will be copied and the user can access them by clicking on *Open folder to access files* directly from the interface of MetaDefender Endpoint or from native applications (Windows Explorer, Word, Excel, etc.).

![](https://uploads.developerhub.io/prod/2x2P/oy9sjblpou75i8eoaxy5oql3zr9shx43qqht8xyrgtcwhriix6o4ly5ngygddbhs.png)

A pop-up notification will also display at the bottom right of the screen, indicating that the files/folders were copied successfully.

![](https://uploads.developerhub.io/prod/2x2P/2ic72bx78tagojcif7q9cne0w3db6v6vgfg3i5y7me9a0dw5tyineumvsqu3ipbf.png)

**Step 7:** User can access files through native applications if they’re found clean.

![](https://uploads.developerhub.io/prod/2x2P/beng70udoeo05p7635rew0l3t70d4wzldhzxkm4khl41np85fqub3g96vudwc367.png)

**Step 8:** Users can export and access the scan report by clicking *Report*, then choose the preferred file format: PDF or CSV.

![](https://uploads.developerhub.io/prod/2x2P/yeg3pzzg9ikk6ldgdpvj1ymzwrbxftl60l2fsh9a6id1xcylggvlmheaqy6pn6xg.png)

![](https://uploads.developerhub.io/prod/2x2P/04xrrg46qe33zt9cinr04tjxg6qw6dzj5g85n84x858igs06ghvr89xodw583fgd.png)

**Step 9:** Users can also customize the information to be included in the report. Once done, click *Export*.

![](https://uploads.developerhub.io/prod/2x2P/rv54v1eeuoon6xupqgtx87udlatohudxjphip0c56r1uz0gk0pt20h3i5eugp88h.png)

![](https://uploads.developerhub.io/prod/2x2P/uvovps7gvk26gk5gxrw775mtktmpv2uw67k70g038hebm85d2g30mmksqwelcp9f.png)

**Step 10:** Choose the destination to save the report.

![](https://uploads.developerhub.io/prod/2x2P/eevaxi8ky5rxbqxn799a03iv6m15jj5p8zohwn8uxzppzuibgl74lqc8y7b7iq00.png)

**Step 11:** The report will show up automatically once saved successfully.

![](https://uploads.developerhub.io/prod/2x2P/zylfqhficd60eajrf73cai1gz9qgihotxvfol6y38qplrqcs6ai2hv2bhll5seuf.png)

#### ***Copy files to the USB***

**Step 1:** Plug in the peripheral device into the endpoint’s port, and open MetaDefender Endpoint, navigate to the Peripheral Media Protection feature. Choose the peripheral device you would like to copy files from and click *Copy to.*

![](https://uploads.developerhub.io/prod/2x2P/sn7dr5szzjwdkrd20im6lwrcgglrdmg7v6wgli7h811cfcmbxw3237a3box6vnjb.png)

**Step 2:** Choose the file or folder to copy from the local drive to media. Users can do this by choosing the local drive directly from the user interface of MetaDefender Endpoint or clicking *Open File Explorer* to work locally in Windows Explorer.

![](https://uploads.developerhub.io/prod/2x2P/ukoykc575iz4l8bhs8xerj4owbo9smz744fzye42bsqsbt5v74rlbx4qzzz53nql.png)

![](https://uploads.developerhub.io/prod/2x2P/vdrvyvcbofokctnrfsyxkix0mc4qu3w3lad4pbd5p7pxasggffx1fvxo4qioqqtp.png)

**Step 3:** Choose the file or folder and click *Copy.*

![](https://uploads.developerhub.io/prod/2x2P/5n9t2l6urodi2ctcdsfk653lb3hm3zydyl85hi8c91etsts12cydnd3qhc451erb.png)

**Step 4:** Click *Copy* to proceed.

![](https://uploads.developerhub.io/prod/2x2P/ujjoekqinxjaq8gn2ywqtw7rlnzrw2lqc7ix46uh80seyi6y0e8bf43w5wx7l8ti.png)

**Step 5:** Wait for the scan progress to complete.

![](https://uploads.developerhub.io/prod/2x2P/s0retotqvcbtzp80q6sl4h7b437erf1l5ras9dzept4zpvqa6fdyiopysoxid7og.png)

**Step 6:** Once the scan is complete, users will be notified that files/folders were copied to the USB.

![](https://uploads.developerhub.io/prod/2x2P/j010p5dct0y34dhotzkagokreiige664ic6xdw489q4hvdszybmf9h8sg6zky8iv.png)

![](https://uploads.developerhub.io/prod/2x2P/zb6d0t62z9kbocn4sqd6u7ixn75w85leo3z6p1stvmrrt3ffiw31jbprkwrk3rx6.png)

**Step 7:** Users can export and access the scan report by clicking *Report* and choose the preferred file format: PDF or CSV.

![](https://uploads.developerhub.io/prod/2x2P/cknai69pchkrseho8cnxiqbts90hrrldamiegknr6ov1zz9o9l70kioxwhxct13f.png)

**Step 8:** Users can also customize the information to be included in the report. Once done, click *Export*.

![](https://uploads.developerhub.io/prod/2x2P/4f6s9id97wiyr3i0ky0rxj8gbboia551vagexm8ghmgtcbtphmszxxl7n7gkyhh9.png)

**Step 9:** Choose the destination to save the report and it will open automatically.

![](https://uploads.developerhub.io/prod/2x2P/jy36lqb7r5idksu7jzzv6c3yonffon91g8ympwy843wb5hmwqtopamt014c7xefa.png)

![](https://uploads.developerhub.io/prod/2x2P/iaazsh4pyf2q49ua10gxvxnni8vr4pqwdgxxla3w26vj4eblce1jxsokwtb4im68.png)

> **Info**
>
> MetaDefender Endpoint's peripheral media protection provides strong defenses for non-administrative users. Administrative accounts, however, can still perform some actions with minimal restriction.
