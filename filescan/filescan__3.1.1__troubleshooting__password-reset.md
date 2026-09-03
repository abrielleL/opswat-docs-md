<!-- source: https://www.opswat.com/docs/filescan/3.1.1/troubleshooting/password-reset -->

# Password reset

In order to reset the password of any user (without using the Forgot Password option) an SSH access is needed to the server which is running Sandbox. **Please use this only as a last resort when the administrator password is lost. Changing the password for other users are possible from the administrator menu.** After logging into the server via SSH, the following steps are needed to set the password of an arbitrary user:

### [Step 1.](/docs/filescan/3.1.1/troubleshooting/password-reset#step-1)

Navigate to the installation directory (usually: /home/sandbox/sandbox) and check if you are in the correct folder by issuing the ls command. You should see that the current folder contains the launch_webservice.sh and shutdown_ webservice.sh files.

BashCopycd /home/sandbox/sandbox
ls
### [Step 2.](/docs/filescan/3.1.1/troubleshooting/password-reset#step-2)

Create a simple text file called email.txt and insert the email address of the user you want to reset its password. Also create a simple text file called password.txt and insert the new password for the user. Make sure the password fulfills the requirements (you can check it on the registration page).

BashCopyecho admin@opswat.com > email.txt
echo Newpassword:1 > password.txt
### [Step 3.](/docs/filescan/3.1.1/troubleshooting/password-reset#step-3)

Shutdown the webservice and wait until shutdown is complete. Start the webservice.

BashCopy./stop_sandbox.sh
./start_sandbox.sh

The email.txt and password.txt files should disappear and now you should be able to login with the new credentials.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
