<!-- source: https://www.opswat.com/docs/supply-chain/configuration/microsoft-teams-notifications -->

# Microsoft Teams Notifications

To configure a Microsoft Teams Connection that can be used to generate notifications on a designated channel for each specified vulnerability after every scan, navigate to 'Settings' menu and go to the 'Network' tab:

![](https://uploads.developerhub.io/prod/jdK6/79fjwalgj7x4oj9lvifq1bjhelloi4968by96m1f2ook85gpy73sc57j2urbgj58.png)

To add a Microsoft Teams Connection**,** click on "Add Microsoft Teams Connection" button:

![](https://uploads.developerhub.io/prod/jdK6/9i15caseilo9w6gnbeetpcyr3cbzodpt5rkn3hpjtwqoc0tw3djfdk7ussuiabgi.png)

Fill in the required fields: give the connection a name to easily identify it later and add a valid Webhook URL. In order to generate the Webhook URL, there are 2 options:

1. Externally, using Microsoft Power Automate: Go to [Power Automate](https://make.powerautomate.com/), create a workflow and configure workflow steps. Example:

![](https://uploads.developerhub.io/prod/jdK6/rb9l7uwq894i4mv48enctysmm7nb0ifoybq3dfmq3e42vixgef6x7ct6np3elnwx.png)

After finished, copy the trigger URL and insert it in MDSSC, in Add Microsoft Teams form.

2. Inside Microsoft Teams: In Microsoft Teams, right click the designated channel and Select Workflows from the dropdown menu. Configure the webhook as following:

![](https://uploads.developerhub.io/prod/jdK6/dlw4lz77ww8nqu5mu58mlh84ulqfj3tgm030i18sb835lws75i5wnz7a5r1l0hxl.png)

When done, copy the webhook URL and use it in MDSSC.

After filling in the Microsoft Teams form, click on the "Add" button. MetaDefender Software Supply Chain will test if the provided credentials are correct and if they are accessible, the configuration will be saved. After that, the Microsoft Teams Connection will be listed in the 'Network' tab, and a confirmation notification will be sent in the channel:

![](https://uploads.developerhub.io/prod/jdK6/ux1l624tx63n791aa2xzhrejsw76atxf4enq430spbeof66n52zpkjnno2h8r2yc.png)

> **Info**
>
> Multiple Microsoft Teams Connections can be registered. Only one per workflow can be used for notifications.

At this point the Microsoft Teams Connection can be edited by clicking the three-dot button and by selecting "Edit" option which will open the same form that was used to add the connection in the previous step.

![](https://uploads.developerhub.io/prod/jdK6/jqfh6cd3gxec0bxmdbolejh0js7xs6r77vmx606hhwi037bctonm8260gk4bih2i.png)

Microsoft Teams Connection can also be deleted if it is not used by a workflow. Otherwise, an error will appear:

![](https://uploads.developerhub.io/prod/jdK6/ysesutekidf518v49doof47qnms66dwirwrkz278d6qwov40bv34z1chrfq7hf3j.png)

After a successful scan, a notification should be received on the selected Microsoft Teams channel, highlighting the scan report findings.
