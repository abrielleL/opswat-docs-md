<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-okta -->

# Provision Users Through Okta

1. On the Okta Admin login splash page choose “Create a new app”.

![](https://uploads.developerhub.io/prod/97qW/xuadmsk02989ipkwpg219gwbqmsi6b2u1jvedfg23j3htwsl3adojld8hnwwzpr7.png)

2. Choose Web and SAML 2.0.

![](https://uploads.developerhub.io/prod/97qW/tnji1xw0cb1z1zh9pb3tm8b54dbb3gy07pwlyu08s0fl6s02zivaxpl0dx7whq45.png)

3. In the “App name” field, fill in “MetaDefender IT-OT Access” or something similar. You can also upload a logo if you like. Do not check the “App visibility” checkboxes. Click Next to continue.

![](https://uploads.developerhub.io/prod/97qW/2sgz50cmdrxg770bgnnuecdveqkg8wouzozn92a1gb1iwrwom1ma64177pdcfu6k.png)

4. Under the “SAML Settings” , fill in the “Single Sign on URL” field with a properly formatted URL as a placeholder. Note You will change this later after retrieving the applicable value from MetaDefender IT-OT Access.
5. Leave the box checked next to “Use this for Recipient URL and Destination URL”. Leave the box unchecked, next to “Allow this app to request other SSO URLs“.
6. Fill in the Audience URI: eg “metaaccess-sp”.
7. Default setting are fine for “Default Relay State”, “Name ID format”, “Application username”, and “Update application username on”.
8. Skip the first “Name” and “Value” fields.
9. Under “GROUP ATTRIBUTE STATEMENTS (OPTIONAL)”, fill in the “Name” and “Filter” fields.
   1. For “Name” enter whatever you want but save the value to use later in the MA UI”, eg: “groups”.
   2. Under Filter , choose “Matches regex” and “.*”
   3. Advanced users may choose other options but it’s recommended to use these setting unless you’re very familiar with Okta.

![](https://uploads.developerhub.io/prod/97qW/ekwgl6xosobhy2ol2i96ulg4wwywjrnmfke0zvk9w9jmb593wu37lswf5dkr4f3k.png)

10. Click “Next” to continue.

![](https://uploads.developerhub.io/prod/97qW/urgcwr7rut55icpv7i070sebh5e16yhpwwpvywo2puk36122gz7evpro3vlymwts.png)

11. The next page is just feedback for Okta, and has no functional impact. You can choose “I'm an Okta customer adding an internal app”, then leave all the other fields blank and click “Finish”.
12. On the next page (under the “Sign On” tab), in the Info Box labeled “SAML 2.0” there is a link called “Metadata URL”. Click Copy, open new tab and paste that url, press Enter. Save as metadata.xml file you will import into MetaDefender IT-OT Access.

![](https://uploads.developerhub.io/prod/97qW/1wevyrz55m4ccunt19f8qtx2em25dbno00dv3cmgy8icuvtpe3nkh25tb4bblxnt.jpg)

13. Log into your MetaDefender IT-OT Access Console at [https://www.opswat.com/products/metadefender/it-ot-access](https://www.opswat.com/products/metadefender/it-ot-access).
14. Navigate to User Management > SSO > SDP and check “Enable Single Sign On”.

![](https://uploads.developerhub.io/prod/97qW/l4fk0v81d81pc86y6ixrifjgi7w3t333d77xb8rkmaqj7jzw5ehhj8rf2d7dr3rn.jpg)

15. Next to “Import configuration from XML Metadata file”, click “Choose File” and upload the “metadata” file you just downloaded from Okta. This should automatically fill in the “Current Certificate”, “Issuer”, and “IdP SSO URL” fields.
16. In the “IdP Name” field, enter “Okta” or some other string. This is only for reference in the MetaDefender IT-OT Access UI.
17. Leave the Logout URL and Error URL fields blank.

![](https://uploads.developerhub.io/prod/97qW/nmjozscytruvm1n6hyhro9dpary0mvh6kigk1y2yxaz8hfcii2lmvva2sfm2ri5c.jpg)

18. At the bottom, click “Add Group Attribute” and enter the value the value from the “Name” field in Okta. Presumably something like “group”.

![](https://uploads.developerhub.io/prod/97qW/bhpjk3xv3si89mqsuh9zbutooxknwqr99huyt5jd5v1i0xft96anh6xdxhkcjv2r.jpg)

19. Scroll to the top of the page, click “Save” and enter your MetaDefender IT-OT Access admin PIN.
20. At the bottom of the page you will see a new value called “MetaDefender IT-OT Access Login URL”. Click “Copy to clipboard”.

![](https://uploads.developerhub.io/prod/97qW/9ks34v4hc7cw0kuhrhnb0vjonybkuo477e56ld5dgwl5ofd6wc0qemreqsnt0da0.jpg)

21. Switch back to Okta, click the “General” tab, scroll down to “SAML Settings” and click “Edit”.

![](https://uploads.developerhub.io/prod/97qW/z9uqjprzoumqqgbsgo54bf3cutyxk0e62cd64cqd0a78i33m9b8qhpp7lawcsna8.jpg)

22. Click “Next” on the first panel.

![](https://uploads.developerhub.io/prod/97qW/v198auwap3m0ehdh0mu7q7cshrko4h2oapjxvc52y2hlspq07clikpke7uq6flda.jpg)

23. There will be a placeholder URL under “Single sign on URL”. Replace this with the URL you just copied from MetaDefender IT-OT Access.

![](https://uploads.developerhub.io/prod/97qW/frb4ipdm4m9isk5c5ydzoh34c5gomimm5vghp6qcetks7c79gsk8h0065kseyegn.jpg)

24. Scroll to the bottom and click “Next” and then “Finish”.

![](https://uploads.developerhub.io/prod/97qW/23uw6649t6a5te4kljmygctuv5s7mjgvgzgaszxvvuq2sl9px7vyj7tv7a0oyvsu.png)

![](https://uploads.developerhub.io/prod/97qW/y9rmlsubqackeu8qidh7ssq506sw458yufsgasuse8mhbp31cm7wyudyo8zq1b2f.png)

25. In the navigation bar on the top, mouse over Applications and click the Applications link. Then click the Gear icon next to the MetaDefender IT-OT Access app, and choose “Assign to Groups”.

![](https://uploads.developerhub.io/prod/97qW/y0cs273p8wlb18691ydf7enlbjwejpo63aqlfb8gdmpi3933potpbqp9cjbwej86.png)

26. On the groups panel, you can decide which groups you want to use for assigning SDP access in the MetaDefender IT-OT Access console. Click “Assign” next to each SDP user group. Note You will need to record the selected group names for use in MetaDefender IT-OT Access. Please copy and paste the group names to minimize human error!
27. Click “Done.”

![](https://uploads.developerhub.io/prod/97qW/c80gw9kutcs26mgldbq1cljessvknm3tpxn7suymnmbsezdkd5ku37usuhn4ghcp.png)

28. Navigate to the MetaDefender IT-OT Access console at [MetaDefender IT-OT Access](https://www.opswat.com/products/metadefender/it-ot-access), then go to User Management > IdP Groups, and click “Add”.
29. Fill in a group name you copied from Okta, enter your PIN and choose Add. Your new group will show up in the “IdP Groups” section.

![](https://uploads.developerhub.io/prod/97qW/bpn190b5l57dgab28w585w92zum2vmvz4547esv7zw61810y5mh6tjzqtd10n9s8.jpg)

30. Repeat for each SDP user group in Okta.
31. When you are ready to assign your new groups to protected applications, go to Secure Access > Protected Apps, click the “Assign” link next to your desired application(s).
32. On the “Assign End Users/IdP Groups to Protected Applications” Move groups “Available Users/Groups” to “Selected Users/Groups” to assign access, then enter your PIN again and choose Enter.

![](https://uploads.developerhub.io/prod/97qW/va2rj508e35t4qvdq1igue74rihjrrr6z858pkbetcakjg0gxtvp5c3uwc0qdkn9.png)

33. Log back in to the Okta console as an end user and click on the “MetaDefender IT-OT Access” application.

![](https://uploads.developerhub.io/prod/97qW/r30j3zlw9u87vay0rx7hoi78wojmxob90lxabf5pdih60ikummwbhu4caelq20p5.jpg)
