<!-- source: https://www.opswat.com/docs/supply-chain/operating/github -->

# GitHub

### How to Configure Webhook

1. Log in to the GitHub account and navigate to the repository that requires event based scanning triggering.
2. Navigate to the repository "Settings" menu, see example below:

![](https://uploads.developerhub.io/prod/jdK6/7pdrdfkoobady5y7djceew4jbbousdekxyuz7j5wh807esc9bmc4ywmgf8sin5hg.png)

- Once on the settings page, in the left menu panel choose "Webhooks" under the "Code and automation" category;
- Click the "Add webhook" button in the right top view of the Webhooks panel;

![](https://uploads.developerhub.io/prod/jdK6/g9mq0hw5eke8y6e6txxxtm21cckhxa3i61yk1qkar4zfe5orwf2ny59ukytqhmli.png)

4. The following webhook configuration page will be opened :

![](https://uploads.developerhub.io/prod/jdK6/zu9ayjvdkqlh05w4elnh376qwioxnk1jwhnwzw0s0uqj1lv1weu7q3hp9qjszpg1.png)

- Here, under the "Payload URL", insert the Webhook URL obtained in MDSSC, how to do this is explained above;
- Change "Content type" to "application/json";
- In the "Secret" field, copy your MDSSC API key;
- If the installed MDSSC does not have a publicly signed SSL certificate, then choose "Disable" under the **SSL verification option.** In this case, the user is presented with the following screen, here is acceptable to click the "Disable, I understand my webhooks may not be secure".

> **Info**
>
> If the SSL verification disabling is not an acceptable option, then appropriate public SSL certificates have to be obtained for the MDSSC instance. Please refer to the documentation in order to install the publicly signed certificate keys.

![](https://uploads.developerhub.io/prod/jdK6/ivos3x1xio4lrbpszbmm7qtgq6y4mmoemznzg2qysi2t7f8ehasiivdvxkyzgveg.png)

5. In the same view further down, it is possible to configure the event trigger types desired, out of the supported ones.
6. By default, "Just the push event" is selected. If it is necessary to configure triggering based on pull request open or merge, click "Let me select individual events" option, which will open a list of events, ex:

![](https://uploads.developerhub.io/prod/jdK6/l539pa2w15kcb0lri9py2twp891zlsg8pzhhq3vi3z3hcoyhmwa2xqkfjov146tv.png)

7. Out of the list of events, MDSSC supports only the ones described above, and selected in the below example:

![](https://uploads.developerhub.io/prod/jdK6/6ige270dtft2d45ot01af01hjq3mnt8l5wxd2siv5a8ek3rvlp4vrsejwabx6r3b.png)

8. After the desired event types were selected, ensure that the "Active" option is ticked.

![](https://uploads.developerhub.io/prod/jdK6/w7aj6crxxs9l3yh603qzaokk036zog5gfpf27lv0gxqa4muwj7up7vojkw3znqfa.png)

9. When finishing configuring the webhook, push the "Add webhook" button.
10. To test the webhook, create a test branch and trigger the selected event type.

### GitHub Ping Event

After setting up the webhook and clicking "Add webhook", GitHub will automatically send a ping event to MDSSC, to test the connection. When this happens, you can see the following notification:

![](https://uploads.developerhub.io/prod/jdK6/fdmthknmj62l97c9sx15c8bchnwtqpgjump27roak80ty74l65fmuzlnnv3ujznx.png)

In order to view the results of the ping event, follow the next steps:

1. Press the "Edit" button on the webhook card:

![](https://uploads.developerhub.io/prod/jdK6/jgn3ami0sidbtalt3avl8p8gwvhnlab658v7q37ti81kwpvkhbob3x6v828ymv0b.png)

2. In the opened menu, navigate to "Recent Deliveries":

![](https://uploads.developerhub.io/prod/jdK6/i53i0bc361jg3j35s94y63fdv3ysdqbllj2yha4je078r6ntrxplhtejoyeyamzq.png)

3. Click on the ping event:

![](https://uploads.developerhub.io/prod/jdK6/p7l9ykhd67vivuq6w6rgltuddyp7ztur9x6khifkokmhhcxtk5hnu2l8j7g2liyq.png)

If the webhook setup was completed successfully (explained above), the ping request should return a 200 Response. Example:

![](https://uploads.developerhub.io/prod/jdK6/epkczlmri02d6db7v5mhm98i1zf5fsdo4up7ovxdewn8iuziv2dfqe16bqn80yd8.png)
