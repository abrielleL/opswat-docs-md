<!-- source: https://www.opswat.com/docs/supply-chain/configuration/syslog -->

# Syslog

To configure a Syslog server for sending logs to an external syslog server, navigate to 'Settings' menu, and go to the 'Network' tab:

![](https://uploads.developerhub.io/prod/jdK6/wkjrdoph6zf9x0orouhbiq01ydtmkvfymkyf7rksaws9a7je14b0fv6pjgut5ov4.png)

To add a Syslog server configuration, click on "Add External Logger" button in the "External Logger Server" section:

![](https://uploads.developerhub.io/prod/jdK6/rtelfg7swfrzyowv3pocusq2frw4j8xjt82y45bchpzzgy2cpghhuuaehj5eqas5.png)

Fill in the required fields, example:

- Server Address: Enter the IP address or hostname of your syslog server
- Port: Specify the **UDP** port number
- Facility: Choose the appropriate syslog facility (e.g., Local0, Local1)
- Format: **RFC5424** (standard syslog message format)

![](https://uploads.developerhub.io/prod/jdK6/3r9i0wheqsblxe1e2776k82unonwkwo9xjqyhr6pek80vfpgwc7qamjvyfx52ave.png)

Once configured, logs will automatically be sent to the specified syslog server.

> **Warning**
>
> By default, **only** high-priority **audit** logs will be sent to the syslog server.

---

To edit or remove an existing syslog server, locate the server in the list, click the **three dots** button, and select either "**Edit**" to modify the configuration or "**Delete**" to remove the server.

![](https://uploads.developerhub.io/prod/jdK6/zh65gz4sccskodaret7cez8j1xj6li8wuc7kwpozwfqdecagzdr2rhxji3blqaak.png)
