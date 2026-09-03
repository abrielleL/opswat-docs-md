<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-google-workplace-gsuite -->

# Provision Users Through Google Workplace Gsuite

This section shows you steps to integrate with GSuite for SDP end-users authentication into MetaDefender Endpoint.

> **Info**
>
> These instructions assume that the MetaDefender Endpoint is installed, and that your device is part of a MetaDefender IT-OT Access group with SDP enabled.

> **Info**
>
> **Please note:** Google estimates that any changes made via the Admin Console can take up to 24 hours to propagate. If your changes do not take effect after 24 hours, please contact Google Support.

- Log in to your [Google admin console](http://admin.google.com/) and click on “Security” > “Context-Aware Access”.
- Click Access Levels, then “CREATE ACCESS LEVEL”.

![](https://uploads.developerhub.io/prod/97qW/pf3y95fiavkulgxa6clh1sczzbgxyxoa12e484i5a4c3i6w17txf8ebwmfgkqfo0.png)

- Give the new rule a name, like “MetaDefender IT-OT Access SDP Gateway” and click “Continue”.

![](https://uploads.developerhub.io/prod/97qW/vka5w9ul3rzieh3wryzek409zp0d22xlahg7uyq55ag5frttpsji3thfo1050pxg.png)

- Ensure the “Meets these conditions” radio button is selected, and click “Add attribute”.
- From the left side pick menu, choose “IP Subnet”. On the right, enter the outside IPs of your MetaDefender IT-OT Access SDP Gateways, comma-delimited.
- If you are using the OPSWAT Hosted Gateway, enter the single IP, 52.14.220.48 instead.

![](https://uploads.developerhub.io/prod/97qW/hgawi41mnnrkipgk3ikgq5jvzbdeikztc68s3g6do74cybc4pyzdp5wcdpu748x7.png)

- Click “Create Access Level”. You should see a green check next to “You've created an access level“.

![](https://uploads.developerhub.io/prod/97qW/q3vl3jwpuyhq06ytquul9biwj5c32a5sl2d8inw68rbtw3uz2dvmtfwptfyldach.png)

- Go back to the main Admin interface and click on “Security” > “Context-Aware Access” > “Assign Access Levels”.
- Check the selection box to the left of the apps you want to control.
- **Important:** For initial testing we recommend selecting a single app that’s not critical to your operations. Once we verify connectivity to that app, you can come back to this interface and add the Access Level to other apps at your convenience.

![](https://uploads.developerhub.io/prod/97qW/alzlqy2r2ahxpr01s5x9x1xxqj5qsv7jaxiczh6cj19lwwg2iwgau0vt0t8ryo1o.png)

- Click “Assign” at the top of the app list, then choose the Access Level you want to apply and click “Save”.

![](https://uploads.developerhub.io/prod/97qW/jrr31s5x0423rxq4mt2k2it2of2lnq5er4my90vvocharpp2s29smm03b2ttgpek.png)

- In the “Access Levels” column, you should now see your new Access Level applied to the app(s) of your choice.
- Go back to the main Admin interface and click on Apps, then SAML Apps.

![](https://uploads.developerhub.io/prod/97qW/7sk674q9xt59tyxi0m6m8d4f11csmravn7rdrr7txsz44zkgv8tmjkw68kr1w310.png)

![](https://uploads.developerhub.io/prod/97qW/l7tc787kips2h3inhbzc1nq2bfdyv84wnu4216qx4cwynsaucbj0vylmfrrc057v.png)

- Choose “Add App”, then “Add custom SAML app”.

![](https://uploads.developerhub.io/prod/97qW/xs2vmyiw1igbvpvgctwovdtednlad4kw96c1yfdjqr9f18stfyuun0jxe30g4n07.png)

- Name your app, e.g. “MetaDefender IT-OT Access SDP” and click Continue.

![](https://uploads.developerhub.io/prod/97qW/xctdz2x0p74qyv6rif7mslam0hjudujaffarpx7s71i41duzw345otefrd2gumj8.png)

- Click “Download Metadata”, then Continue.

![](https://uploads.developerhub.io/prod/97qW/ogc3nblcz0mu4t6xk9prz984nw6lwti77rd4gc08nzwiv8m7a86fvvlqk7htglve.png)

![](https://uploads.developerhub.io/prod/97qW/kvxgopil7nrlqx2vdo9jj3fjwxoxk8wl7t4emyxynjw3ezfzvpasquihbsmk5fpz.png)

- Open your [MetaDefender IT-OT Access console](http://gears.opswat.com/) and click on “User Management” > “SSO” > “SDP “.

![](https://uploads.developerhub.io/prod/97qW/sy91qkqrqmj8ndzilkufis68imr09habw0vbym5bz844ugqx053mg8dbyj2ql6f8.jpg)

- Next to “Import configuration from XML Metadata file“, click “Choose File” and upload the Google metadata.
- Copy the URL next to “MetaDefender IT-OT Access Login URL“, enter “group” in the “Group Attributes” box, and click Save a the top right.

![](https://uploads.developerhub.io/prod/97qW/ehs63wvunzd1267taik4ly4pfay61hhuvp3vb63fqnorwd8izr74qm7qx5e4ow7f.jpg)

- Go back to the SAML app in Google and paste this URL as the “ACS URL”, then enter “metaaccess-sdp“ as the “Entity ID”. All other values can remain default.

![](https://uploads.developerhub.io/prod/97qW/uydlu7yprhe5hc8gdhg3ww2d7qkrrt3qpp2bnim4e2tea8l0rx3u9skc4lln6kg5.png)

- Click Continue.
- Click “Add Mapping”.
- Under “Google Directory attributes“, click “Select Field”, and choose “Employee Details” > “Department”.
- Under “App attributes“, enter “group”, and click “Finish”.

![](https://uploads.developerhub.io/prod/97qW/nxvcg023v6m2d6f9ckinm4q9psoc1p3bq0b2557cp08q07q9vstmxubcn2u8d49d.png)

- This will bring you to the App details. In the “User Access” card, click “OFF for everyone”

![](https://uploads.developerhub.io/prod/97qW/5jf59gnoctjrzsk6spx4dwcj3p1xpqubh7pks2swm8hlp8txz323blv0e7f3krwn.png)

- On the Service Status page, click “On for everyone”, then click “Save”.

![](https://uploads.developerhub.io/prod/97qW/ih3qh03bzwkll33b7b85grmrsekt7klonmk1atlx7i605kzcadkslppf13iqu4kz.png)

- Navigate back to your new app and click “TEST SAML LOGIN”.

![](https://uploads.developerhub.io/prod/97qW/9z0aju4lb27h2ix8fw8hojn5blavo06ebil836atdu2l7vkd4q83dm6ajrm3j8ae.png)

- This will open a web browser and prompt to allow launching the MetaDefender Endpoint.
