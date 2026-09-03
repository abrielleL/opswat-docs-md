<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-manage-devices-by-groups- -->

# How can I manage devices by groups?

> **Check Your Product:**
>
> This article applies to all My OPSWAT Central Management products deployed on Windows, macOS, Linux, Android and iOS systems.

My OPSWAT Central Management allows IT/Security administrators to manage and ensure compliance through their small to vast networks of endpoint devices, with minimal effort and complexity.

To streamline administration, admins can allocate endpoint devices to groups or categories that are associated with unique policies and security levels.

## How to create a new group

1. Log into your **Console** and navigate to **Inventory>Device Groups**.
2. Click on the **Create New Group** button, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/9w3lav9txjzqzj6koseqe1wbh1gegdrmca2ak2uni4rt9k6p5fqemrthduuvmido.png)

3. Fill in the group name and assign a policy and rebranding package (if applicable). **Notification** and **Webhook** settings are not required during the group creation process, and can be updated at a later stage.

![](https://uploads.developerhub.io/prod/97qW/72m6rhqp79lvpkvf8xb762zwgrhtpq4jw0matatgzdt8csn7u84u9yvjks67b2t9.png)

4. For now, click **Next** or **Assign & Next** in the lower right-hand corner of the page until you reach the **Assign Devices** page, as illustrated in the screenshots below.

![](https://uploads.developerhub.io/prod/97qW/uxch4a20uvcg7lww7rlx0uw1zas6tud5igf2r4w2wqot5ng9ujw7208yxga33d12.png)

5. On the **Assign Devices** page, use the search field or **Filter** button (illustrated in the screenshot below) to search the device inventory for the required devices, or simply browse the list.
6. Once located, check the selection box alongside each device to be added to the group, also illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/isqe4na8nks1stomhg8o51qowpc5io17nhn0wwmevkng6hz7nf5xuruh4r9w2rss.png)

7. Finally, click the **Create Group** button to apply your settings, and enter your PIN to confirm, if prompted.

## How to update a group

1. Log into your **Console** and navigate to **Inventory>Device Groups**.
2. Click on the group you would like to update to access the device group details, then click on the **Settings** tab.

- To *update the group name*, simply change the name in the **Name** field, as illustrated in the screenshot below.
- To *assign a new policy to the group*, expand the option menu alongside **Assigned Policy**, then select the policy you’d like to apply, as illustrated in the screenshot below.
- To *configure additional settings*, toggle the switches to their enabled state, as illustrated in the screenshot below.

3. Once configured, confirm your change by clicking **Save** and  entering your **PIN** as prompted.

![](https://uploads.developerhub.io/prod/97qW/raz9yy4je2aid0a3n02dhn1x92p2fvhzom3ctzfz55qn3a3n4e82acn7j7du7l0u.png)

> **Please Note:**
>
> Following a group policy update, My OPSWAT Central Management will reassess the device status of all devices in the group, to confirm whether they are fully equipped to apply the rules associated with the new policy.

## How to assign devices to a group

To assign new devices to an existing group, there are three options.

- Option 1: manually via the **Device Groups** list
- Option 2: manually via the **Devices** list  (Windows and macOS only)
- Option 3: automatically enroll devices to a group

### Option 1: via the Device Groups list

1. Go to **Console** and navigate to **Inventory>Device Groups.**
2. To *assign new devices to the group*, click the **Add Devices To Group** button in the top right-hand corner of the page, as illustrated in the screenshot below.
3. Next, check the selection boxes alongside the devices you wish to add.

![](https://uploads.developerhub.io/prod/97qW/kaiy9aum792j14q7gg1baaol2tthepgbh188kglkn98gsuj20rj363ebrm393uvo.png)

4. Confirm your changes by clicking the **Add Devices To Group** button, which will now be in the bottom right-hand corner of the screen.

### Option 2: via the Devices list (for Windows and macOS devices only)

To *assign devices to the group* from the **Console>Inventory>Devices** list:

1. Go to **Console>Inventory>Devices.**
2. Use the **Search** field or **Filter** button to narrow down your options (if required).
3. Once located, check the selection boxes alongside the required devices, as illustrated in the screenshot below.
4. Expand the **Actions** option menu in the top right-hand corner of the page, also illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/uh8nyz5mo2j84e5ocfhahyxd80w5uqy5ild00k8vcb4i600fy1qhw855iu05pr4r.png)

5. Select the **Assign to Group** option.
6. In the pop-up, select the appropriate group from the option menu.
7. Confirm your selection by clicking the **Assign** button, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/bnpei8wntcv475id5boxqxh8y0upaeo8yx8nldzkfnmujnbqg0etf85dos2q4znx.png)

### Option 3: automatically enroll devices to a group

This option allows administrators to enroll devices to a specific group automatically, via device installation package or device domain.

To enroll devices to a group *via installation package*:

1. Log into your **Console** and navigate to **Inventory>Devices**.
2. Click the **+Device** button in the top right-hand corner of the screen, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/ufy49nxz9frcc948220v8uh0s1utw67yk2kduifczazt0eeg3bnfbyowxu8soxhy.png)

3. In the pop-up window, check the **Devices will automatically be added to this group** box, then select the appropriate group from the option menu, and click the **Download** link, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/x5abyu7vqh9scabbmye3crddspoit1wrus3qf6cgmhwrs92o47kxy1jwe41pso5l.png)

To learn more about this option, please [Read This](https://www.opswat.com/docs/cm/configuration---management/device-group-auto-assignment).

> **Pro Tip:**
>
> For Android and iOS devices, the GroupID can be entered when the device is enrolled to an account.

To look up a GroupID:

1. Log into the **Console** and click the **+Device** button in the top right-hand corner of the screen, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/oo7bw4yjvwwso1wiqmj75i8tuw1cycupkw2xsrpdm577cylrr0yw7y0pmc8k6dqt.png)

2. In the pop-up window, check the **Devices will automatically be added to this group** box, then select the group for which you’d like to look up the GroupID.
3. Click the **Download** link, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/pj9h1u0p727np13003ab4ko9h3q1u21qvzxvzrv5nrof1xdx91p0v9xuliv2ai8e.png)

4. You will be redirected to the device group download page, where you should click on the **Mobile & Chrome OS** tab to view the **Registration Code** and **Group Identity** alongside the Captcha at the bottom of the page. See the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/oo8hv3kp76ixzqvenxuzm00kvftlxh7ofm94fp0s8ksjmnf0hm8lq5bz1we6g0fb.png)

## How to retrieve a list of devices in a specific group via oAuth API

Administrators can use the **Get Devices** API, but filtered with the **Group ID** parameter within the request body. This will retrieve a list of all devices within the specified group.

To learn more, please [Read This](https://www.opswat.com/docs/cm/developer-guide/get-devices) and [This](https://www.opswat.com/docs/cm/developer-guide/apis).

> **Support:**
>
> If you have followed the instructions above but are having difficulty **Managing Your Endpoint Devices By Groups**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
