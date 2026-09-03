<!-- source: https://www.opswat.com/docs/mdss/configuration/web-interface-port -->

# Web interface port

MetaDefender Storage Security's web interface normally uses port 80 (for regular web access) and port 443 (for secure web access). If you need to use different ports, follow these steps:

## [For Linux Users:](/docs/mdss/configuration/web-interface-port#for-linux-users)

1. Open the Configuration File:

   - Having elevated privileges, use a text editor to open the file located at `/etc/mdss/customer.env`.
2. Change the Port Numbers:

   - Find or add these lines:

     - `WEB_PORT = 80`
     - `WEB_PORT_SSL = 443`
   - Replace `80` and `443` with the new port numbers you want to use.
3. Save the Changes:

   - Save the `customer.env` file.
4. Restart MetaDefender Storage Security:

   - Open a terminal and run this command: `sudo mdss -c restart`

## [For Windows Users:](/docs/mdss/configuration/web-interface-port#for-windows-users)

Setting up a custom Web interface port can be done either during the installation process ([Windows Installation](/docs/mdss/installation/windows-installation)) or after the installation by following the steps below:

1. Open the Configuration File:
2. - Having elevated privileges, open the file `C:\Program Files\OPSWAT\MetaDefender Storage Security\config\customer.env` using a text editor like Notepad.
3. Change the Port Numbers:

   - Find or add these lines:

     - `WEB_PORT = 80`
   - (Optional) If running on HTTPS

     - `WEB_PORT_SSL = 443`
   - Replace `80` and `443` with the new port numbers.
4. Save the Changes:

   - Save the `customer.env` file.
5. Apply the Changes and Restart:

   - Open powershell.
   - Run these commands:

     - `cd "C:\Program Files\OPSWAT\MetaDefender Storage Security\scripts"`
     - `.\mdss.ps1 -c refresh`
     - This command will refresh the environment variables and restart MetaDefender Storage Security.
