<!-- source: https://www.opswat.com/docs/cm/knowledge-base/how-can-i-capture-custom-information-from-end-users- -->

# How can I capture custom information from end-users?

> **Check Your Product:**
>
> This article applies to all Persistent MetaDefender Endpoint releases deployed on Windows, macOS, Linux, Android and iOS systems.

My OPSWAT Central Management is able to capture custom information such as email addresses, Student IDs and telephone numbers from endpoint users.

Administrators have the option to specify the nature of the information required, and to validate it using a regular expression string. These regular expression strings can be tested and validated using online regex testers like [This One](https://regex101.com).

## How it works

My OPSWAT Central Management will ensure that the endpoint user inputs their information via a non-optional action prompt, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/17n2huo2u1b64jhk3qqf6uyoso4gjlboe7oyegm0w302q5hwngoyf5h4wx6ll855.png)

Once the user inputs their information, the system reports it to the My OPSWAT Central Management backend servers.

Administrators can then view the information via the **My OPSWAT Central Management** **Console**, by navigating to **Inventory>Devices>Relevant Device>Device Details View**, where the data will be listed under **System Information**.

Administrators also have the option to search the device inventory by inputting client information, such as an email address, into the **Search** field, as illustrated in the screenshot below.

![](https://uploads.developerhub.io/prod/97qW/b690qnejpbaz2hc52ez7z1xyrwxaqmyay6nqfe7hn5wi2l9py0n50mkzlkgkwvir.png)

Once enabled, it will take between 1 and 60 minutes before the user is prompted to input their custom information, which period is based on the frequency of Client check-ins with the My OPSWAT Central Management backend servers.

> **Please Note:**
>
> For new MetaDefender Endpoint installs, the first MetaDefender Endpoint check-in will only take place once the installation is complete, the MetaDefender Endpoint is running, and the Client device is properly registered to a My OPSWAT Central Management account.

## How to enable custom information capture

1. Log into the **My OPSWAT Central Management Console** and navigate to **Settings>Global>Advanced**.
2. Check the option to **Enable custom information capture**.
3. Fill out the required fields, including a regular expression string and a message that will be displayed in the prompt to your endpoint users.

![](https://uploads.developerhub.io/prod/97qW/j0r3q2eu9r8maatju6ga4kdl3glz0ntrdrw6werrdbe0r5s8p5khkhsvla8srm54.png)

4. Finally, click **Save** to apply your settings.

## How to update your regular expression string to validate user input or the message displayed to your endpoint users

1. Log into the **My OPSWAT Central Management Console** and navigate to **Settings>Global>Advanced**.
2. Under the option to **Enable custom information capture**, update the regular expression spring or message as required.
3. Finally, click **Save** to apply your changes.

> **Please Note:**
>
> If you make changes to the regular expression, the system will prompt endpoint users to re-enter their custom information.

## How to enforce end users to re-enter their custom information

1. Log into the **My OPSWAT Central Management Console** and navigate to **Inventory>Devices**.
2. Filter for endpoints from which you wish to recapture custom information.
3. Once located, check the selection boxes alongside the appropriate devices.
4. Click on the **Actions** drop down menu in the top right-hand corner of the page, as illustrated below.

![](https://uploads.developerhub.io/prod/97qW/9u3ztzq09yiznfrimunjb8fci8qdjj3urqslwc3dx3so3rhs02my265q3eyriwjz.png)

5. Click on the **Re-Identify** option, then confirm your selection as prompted.

![](https://uploads.developerhub.io/prod/97qW/jzxj2rydf6ibsi5110ozut9m8g4rwhx9ub61ncikpvec4ucz5fwc5bxvgtb6ju8c.png)

## How to clear all captured custom information

1. Log into the **My OPSWAT Central Management Console** and navigate to **Settings>Global>Advanced**.
2. Uncheck the option to **Enable custom information capture**.
3. Click **Save**, then confirm your selection as prompted.
4. The custom information capture feature is now disabled, and all captured data will be purged.

> **Support:**
>
> For any queries, concerns or issues around the **My OPSWAT Central Management** **Custom Information Capture Feature**, please open a [Support Case](https://my.opswat.com/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
