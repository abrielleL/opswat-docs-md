<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/provision-users-through-jumpcloud -->

# Provision Users Through JumpCloud

Objective: Configure a SAML IDP for authenticating users in the MetaDefender Endpoint.

> **Info**
>
> In this article you will learn how to:
>
> - Set up and configure Secure Access for IT as a Service Provider (SP) in JumpCloud.
> - Export the resulting connection data from JumpCloud and import it to the MetaDefender IT-OT Access Console.
> - Enable SAML SSO for your SDP end users.
> - Provide access to SDP-protected applications based on JumpCloud group membership.
> - Invoke SDP by logging in to JumpCloud as an end user.

1. Sign up for an account at [jumpcloud.com](http://jumpcloud.com/). They provide free IDP services for a limited number of users. Once you’ve got the account created and are signed in to the administrator console you should see something like this:

![](https://uploads.developerhub.io/prod/97qW/d2skd5jamgt260oddrf25eje0xcuvi55jh2qf3jihfdwvhtyp06rsyqaxg104hke.png)

2. Add a new user using manual entry.

![](https://uploads.developerhub.io/prod/97qW/smgk4aqtg4bzi0anhee1k0euabqqm01bocy47r4su3li7bg13zkf37ndu41c3yo2.png)

3. Fill in details. I’ve specified an initial password here, but you can let it generate a temporary password too. It’s fine to leave all the other tabs with their default settings for now.

![](https://uploads.developerhub.io/prod/97qW/h194pasb53cav0jt5v9zstdvqr44c5t8ysqvwknzekt87r1bbay8tgsf2rn1qmdk.png)

4. Create a group for that user.

![](https://uploads.developerhub.io/prod/97qW/4zsqqhjijrwie59w46co1u9rweth4peakq11erm22vg4xoqtx7gvvlbt5ieea50e.png)

5. Give the new group a name.

![](https://uploads.developerhub.io/prod/97qW/kv7d4qjhsyr31xw4xip2sy6clra5a8g13d0xt860ju7qt0evuxcy05g2yagoeda8.png)

6. Include the user you just created in this new group.

![](https://uploads.developerhub.io/prod/97qW/dcui7srqz3kd54ssvh5knnj6ray7ypyv0z8x81qujqgtzjscg17buo5edwbwndt7.png)

7. Save the group, the rest of the group settings can be left alone.
8. Create an application. This will be a “Custom SAML App”.

![](https://uploads.developerhub.io/prod/97qW/wkbjsbwk6olu2qkqcjelhqtadfvgdx08yjet58m9kjnr61nmrhikq6xnye3fz185.png)

9. Give it some label.

![](https://uploads.developerhub.io/prod/97qW/4e81dy1u0hc8l3c4c486gn1g9iifu52xsgoqassin0gfsji1fs92uwmwzhmlrban.png)

10. Configure the IDP and SP Entity IDs. These are identifiers the two ends are going to use to verify that authentication attempts are coming from and going to the right places. It doesn’t really matter what they are, just remember them for later when configuring MetaDefender IT-OT Access.

![](https://uploads.developerhub.io/prod/97qW/s7gvpijmepaq2xaa8afp6f4j7da0h28r4schixy2gfx2uyqeq7ptr2tfkyxqpsoy.png)

11. Configure the IDP URL. It doesn’t matter what this is, it just can’t conflict with the URL you specified for any other applications you have defined. I’ve changed mine here, but the default would probably also work for you.

![](https://uploads.developerhub.io/prod/97qW/ux4iih2f4j3lvllhqdgih11pb95mhg2l9t3vq8p1axpq1a1wgfu6skf4wvygna1y.png)

12. We’ll come back here later when we have some more information from MetaDefender IT-OT Access. Save your progress so far by selecting “activate”. When you save this application it warns you that you can’t change this later. That’s fine.

![](https://uploads.developerhub.io/prod/97qW/j9gf325uxq7jg0wkzsp4b85ael1n30cpy8pemg7hct0gd0d57zxkui0z0ng05yn2.png)

13. Edit the application you just created, and export the JumpCloud Metadata. You’ll need this to upload to MetaDefender IT-OT Access.

![](https://uploads.developerhub.io/prod/97qW/w6n871a3c1ztg3i1kj23hjgc3k9604ltggm1nltrjtalhqnuj3ul318dol0g4o3j.png)

14. Navigate to the MetaDefender IT-OT Access administration console. Enable single sign-on for SDP. Note that there are two kinds of SAML SSO setup here. The “Console” setup is for logging into the MetaDefender IT-OT Access administration console itself. The “SDP” setup is for logging in end-users to the SDP product. We’re setting up SDP here.

![](https://uploads.developerhub.io/prod/97qW/8qml78p5ia9s5w8ykym8b4yxgjh8iyka3h1j6q8mwia6lqgdg62bpwa2z8bycu6p.jpg)

![](https://uploads.developerhub.io/prod/97qW/ypwejo9y5bfcclfeev3huk9vna9cb7z57tjxnzowikon4xbu03b7ltjjlyn33mtn.png)

16. At the bottom of this form is configuration for Group Attributes. You need to tell MetaDefender IT-OT Access what JumpCloud is going to use as the attribute containing group information. This can be anything, you’ll just need to enter the same thing into JumpCloud later.

![](https://uploads.developerhub.io/prod/97qW/u80w1tsj9v3x9e4w1v8r9tkvn465dnzrx6bmn88it75j4np4ht241sv89kj17wmq.jpg)

17. Copy the MetaDefender IT-OT Access Login URL.

![](https://uploads.developerhub.io/prod/97qW/cbadvwr443q70ryhr6nrtjc2z0taztn2bx0uwo1p9hkl7fi5tmbnwpjin193f2vt.jpg)

18. Save the Secure Access for IT SSO configuration using the Save button in the upper right of the current page.

![](https://uploads.developerhub.io/prod/97qW/ffs7ct7wvzaziktitcfgiz31k8ksxuso0j3p13nruu7n57krey3pbk78tlyvt5d6.png)

19. Go back to the JumpCloud configuration for this application. Paste the MetaDefender IT-OT Access Login URL as the ACS URL.

![](https://uploads.developerhub.io/prod/97qW/838v82l25q9s2z3l5xveg57ebu1k55dhc631sjm2e4yloook8fu1h3w77owrulge.png)

20. Enable group attributes for the application. Make sure to use the same name specified earlier in the MetaDefender IT-OT Access configuration.

![](https://uploads.developerhub.io/prod/97qW/7nhkzizbultl4vjmmiscuwvbpc471tdwr4vtq0ry23ibkumxpmdaav7z28itm27h.png)

21. Add the group you created earlier to this application in the User Groups tab.

![](https://uploads.developerhub.io/prod/97qW/tjg8425fq2sbf744vbdrxs6cjndpzp6z2j0mpiqs8m9snm2fa2tpuhvo83hkipw0.png)

22. Save the JumpCloud application again.
23. The MetaDefender IT-OT Access settings applied to a device depend on what MetaDefender IT-OT Access group it is in. In this case we want to make sure that SDP is enabled for the MetaDefender IT-OT Access group. For this example I only have the single default group. Note that I’ve already got a device in this group. If you need to install the MetaDefender Endpoint and get a device in inventory do so now.

![](https://uploads.developerhub.io/prod/97qW/azykwv7pkm0zj3elcwu72rvdnpuic3yyhhuinq02ycj927pc2ohc62g66uijxjl6.jpg)

![](https://uploads.developerhub.io/prod/97qW/cm0tdyb21woh7e731qx6wcz2jrefjynjz38kjcdwkfe6zoblebmppegp499rgimm.jpg)

24. You should now define the IDP groups. This should match the name of the group used earlier when configuring the group in JumpCloud.

![](https://uploads.developerhub.io/prod/97qW/c7exovb6p2qum4st9ne03vi5u33lkowuun9l9dukpfhed6bpblzzolz6tflzskb2.jpg)

25. Add an IDP Group to act as an anchor for the SAML group within MetaDefender IT-OT Access. The “Identity Provider Group” value should match exactly what you entered as the group name in JumpCloud. The “Name On MetaDefender IT-OT Access” can be anything you like. Some IDPs don’t expose nice names for groups, so this is a chance to give the group a name that is easy to work with on the MetaDefender IT-OT Access side.

![](https://uploads.developerhub.io/prod/97qW/908587axw804soorc97bpm3bhh833fnxya22qn9g12ufaj4cf8km7j08p1qugrjj.jpg)

26. At this point you can add any protected applications. When prompted for what users have access to these applications select the IDP groups you created earlier.

![](https://uploads.developerhub.io/prod/97qW/ueq1yvo5w2oyz6lsaqjka3zlloxjtita208ltz8h2avtqye0ziv4r0iag0tqh8rv.jpg)

![](https://uploads.developerhub.io/prod/97qW/sysjo3lmp889tvkluu09jeejyuic2xmjvkr8aeyx12wasy023vhvk2m3vr8z0bxz.jpg)

27. Log in to JumpCloud as a the user you added earlier. You may need to log out of the administrator console to get back to a login prompt at [https://console.jumpcloud.com/login](https://console.jumpcloud.com/login). You may need to switch to the “User Login” version of this page. If you’re on the Administrator Portal the button in the top left can switch to the User Portal.

![](https://uploads.developerhub.io/prod/97qW/19p6cjnrhws6awldpkd8qwamyt0cn4tbhk4r6smpimsrq3f5eck0k16at9eziqrk.png)

28. Select the MetaDefender IT-OT Access application.

![](https://uploads.developerhub.io/prod/97qW/zb3nouhqtmlqh802ekbsmmsqyy36fkdjbkpflbx08urhfs1wayh29n2oz4uec5yo.png)

![](https://uploads.developerhub.io/prod/97qW/hhsvqvywwh3u38sronfp8ow5ul533ddo19ilarqzf0z9jarndwit5bs71bkmgxrz.jpg)

![](https://uploads.developerhub.io/prod/97qW/9w0fe3lnvlrcpoqc49tri77v1x2pafetq0q41h3v6hsc48l7j8irc66ep1w7ixrr.jpg)

30. SDP should launch and connect. You should have access to that test resource.

![](https://uploads.developerhub.io/prod/97qW/20h89g4edx5f1vir1boebf9050j1an3rqepj33sk8celt03pgt88ffqck16kg9co.png)
