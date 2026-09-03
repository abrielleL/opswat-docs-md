<!-- source: https://www.opswat.com/docs/supply-chain/operating/bitbucket-data-center -->

# Bitbucket Data Center

1. Login to your Bitbucket Data Center UI and navigate to the repository which requires event based scanning.
2. Click the "Repository Settings" button in the left side menu, then under "WORKFLOW" click on "Webhooks", in the new menu entry click "Create Webhook" button found in the top right corner, following screen should be visible:

![](https://uploads.developerhub.io/prod/jdK6/hw292dp25or9vg2sdwgkisnq8zbonruvh1wdeiy8mckugfzzhvi70b9787yusg4h.png)

- in the "Name" field, type in a user defined arbitrary webhook name;
- Copy in the URL field the Webhook URL that was obtained in MDSSC, using the method described earlier;
- In the "Secret" field, copy your MDSSC API key;
- If the MDSSC server does not have a valid SSL/TLS certificate, enable the "Skip certificate verification";
- Proceed to configure the desired events, from the following supported:

![](https://uploads.developerhub.io/prod/jdK6/98d8ey1nqflzu9v1opcfs5fk3ww0dgj33z4inpd038ih3du17qrm9rgr09iys3dl.png)

- Finally click "Save" button.

3. To test the event, trigger it with a push event to a branch that is monitored via a MDSSC workflow.
