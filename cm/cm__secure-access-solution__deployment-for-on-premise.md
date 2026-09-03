<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/deployment-for-on-premise -->

# Deployment for on-premise

## Download and Install My OPSWAT Central Management

Follow the instruction [Onboarding](https://www.opswat.com/docs/cm/deployment/onboarding) My OPSWAT Central Management for on-premises deployment.

## Download and Install Your NAC VM

Please follow these instructions to download and configure the NAC VM.

1. Download NAC VM:
   1. Login to your **my.opswat.com**
   2. Navigate **Product Download**
   3. On **MetaDefender** **NAC** , click on **Download**
   4. Choose **Platform** and **Version 10.x.x**, click on **Download**
2. Follow the instructions below to install and configure the NAC in the admin's virtual environment

## Step-by-step guide

Once the appliance is powered on, connect to the console and login with the username “admin” and the password “admin”.

After logging in, the console configuration utility will be launched. The resulting pages will prompt the user to update the admin password, configure the IP address settings and enter a license key.

### Reset Admin Password

![](https://uploads.developerhub.io/prod/97qW/0m6cvjk7hbfpra59unxtrdxbuq0a5k5tpuv73mgzaeu1gneecjnekf36b932vjpf.png)

### Configure Appliance Network Settings

![](https://uploads.developerhub.io/prod/97qW/nsx3h3sxho3rq6terz2v37kbfn55j4p3v2kdm0dlvrfovjsz5coev8frb0mg1sd2.png)

### OCM Integration

![](https://uploads.developerhub.io/prod/97qW/k7aqpm6fk5w2nedrobe0kzfesrrwwpehw0387r1oh7e10yfziorbybvbp1zdcuof.png)

You can achieve OCM RegCode by:

1. Click on the button Enroll Product
2. Select Metadefender NAC Server

![](https://uploads.developerhub.io/prod/97qW/loijq478gsi6ne7cjk5pn5ugoaj648necxxvf85q460vb15mlh31xvzwm1tznep0.png)

3. Copy the Server URL and the Registration Code then paste to the NAC VM

![](https://uploads.developerhub.io/prod/97qW/rrkaoy810xaesqm565hroi1gqvjbaek4jhnebmwixisoozzmsyt01x5cmi6pebyi.png)

After activate successfully, you will able to move to the last setup step - Time Zone.

### Setup Time Zone

Choose your best match Time Zone. After done setting, the system will restart

![](https://uploads.developerhub.io/prod/97qW/wdpyztycvjb3yqi76cw60uiw1hgs5i38sdvivhrusl5msqsamm0zedkji42xwae3.png)
