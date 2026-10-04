<!-- source: https://www.opswat.com/docs/supply-chain/configuration/resetting-password -->

# Resetting Password

If you forgot your password, you can reset it from the login page.

- Click the **Forgot Password?** link next to the password field:

![](https://uploads.developerhub.io/prod/jdK6/7pn4grblqrwdigbottjp00bc2y231ny04ivdgz09ilqds0dz05d1qaubrurhlc2o.png)

- On the **Reset Password** screen, enter the email address of your account:

![](https://uploads.developerhub.io/prod/jdK6/s57bssrxwfgzedl55xr96s61oo4pvfibb95jou2iovd54cea12f0jkiq8qwdfclq.png)

- Click **Submit**. An email with detailed instructions to securely reset your password is sent to your inbox - open the link inside, choose a new password, and sign in with it. If the email does not arrive, check your spam folder or use the resend link on the confirmation screen:

![](https://uploads.developerhub.io/prod/jdK6/1fqvrlm784vmur09xvdo2k0y5twik8r5zyufgn1i75jelu91gqo4ib5utsttvhdx.png)

## SMTP is required

Password reset emails can only be sent when an SMTP server is configured. Without one, the reset request fails with the error below - see the SMTP page in this section for how to configure it:

![](https://uploads.developerhub.io/prod/jdK6/7vi7h7m2kkdgita57ec4t849gmotflvw1ivfqu0jxydupwnq24xj0d15kxvt17wz.png)

## Account Lockout

Keep in mind that you have limited attempts to log into your account. After 5 failed sign-in attempts within 15 minutes, sign-in is blocked for 10 minutes. The login page shows how many attempts you have left and, once blocked, how long to wait. During this time, sign-in is refused even with the correct password.

 If you have forgotten your password, you can reset it using the steps above. You still need to wait for the block to end before signing in with the new password.

![](https://uploads.developerhub.io/prod/jdK6/i8jhbykef9i5o5v9gip9ossmy744ojgx6jtt0mvtor1aam6jke4xd22ws7esm4p1.png)

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
