<!-- source: https://www.opswat.com/docs/mdss/4.5.2/knowledge-base/windows-deployment--how-to-create-a-persistent-mount-for-smb-and -->

# [Windows] How to create a persistent mount for SMB and NFS?

> **Info**
>
> All the below steps must be performed on the same Windows Server machine where MetaDefender Storage Security is installed.

## Step 1

Navigate to **Task Scheduler** and click on **Create Basic Task** (on the right side)

![](https://uploads.developerhub.io/prod/k8zL/z94a4tvf60ohmyw04xavj4se03ueyxhh9db8duy3440it169740lvvm2lzwu536q.png)

## Step 2

Give your task a specific name and click **Next**

## Step 3

Select **When the computer starts**

![](https://uploads.developerhub.io/prod/k8zL/2kaqlo88qi2u6s0e42jkeu91eduxvnqij3s5klig2u4nfn3jbvwsyw0p8vween6c.png)

## Step 4

Select **Start a program**

![](https://uploads.developerhub.io/prod/k8zL/qzyx6c41bb9g7dnrb3p41fwleorsjh54s6nh3ze890eisxmgy87iqgo5lryrkasz.png)

## Step 5

Enter your mount command in the **Program/script** field.

For SMB mount, below is an example: (the password must be provided here because at startup, Windows will not prompt you for it)

```bash
net use T: \\10.30.160.239\sambashare /user:sambauser sambapassword
```

For NFS mount, below is an example: (no password is required for NFS):

```bash
mount -o "nolock,sec=sys" 192.168.207.139:/srv/company-public-files/ Y:
```

Click **Next -> Yes -> Finish**

![](https://uploads.developerhub.io/prod/k8zL/h0kg0jchjavaq2lug22a6fytdtrbhan6ar6sd9jhymx08w4e5zduprq2hjn567w3.png)

## Step 6

From **Task Scheduler**, navigate to **Task Scheduler Library** -> Select your newly created task -> Right click -> Properties -> General -> Change User or Group -> Advanced -> Find Now -> Choose **SYSTEM** -> Click OK and that's it.

![](https://uploads.developerhub.io/prod/k8zL/p06xlk4jksnn2bsu5diqvfvs5oy7xst4m2o02lfbkfstj4uynii1z3dnx9i7xwvw.png)

> **Warning**
>
> When logged in as a normal user or administrator, the mapped network drive will appear as disconnected. It is not disconnected, the user that is logged in does not have privileges to access it. If you open a terminal as a NT SYSTEM, you will be able to access the newly mapped network drive.

![](https://uploads.developerhub.io/prod/k8zL/b3gii29783mgwsqygvcxolmn2ssh4q3keng8url3bnbuhtxowufxojcfbb1n8ld9.png)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
