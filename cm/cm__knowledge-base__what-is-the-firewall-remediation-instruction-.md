<!-- source: https://www.opswat.com/docs/cm/knowledge-base/what-is-the-firewall-remediation-instruction- -->

# What is the firewall remediation instruction?

Steps to enable firewall on your device:

1. Turn on your firewall on at least one of your firewall products: follow any guidance from your organization or Firewall vendor to turn your firewall on. Below are some references:
   1. [Windows Defender Firewall](https://support.microsoft.com/en-us/help/4028544/windows-10-turn-windows-defender-firewall-on-or-off)
   2. [Mac OS X Firewall](https://support.apple.com/en-us/HT201642)
   3. [Linux Firewall](https://www.tecmint.com/start-stop-disable-enable-firewalld-iptables-firewall/)

> **Please note**
>
> If the Windows Firewall has still been detected as disabled, please make sure to disable inbound/outbound rules that allow all connections.
>
> ![](https://uploads.developerhub.io/prod/1yda/2o0s64x74umidj7sm3oe60rh49l575nd9xr66mm6ubf96lkim79v9dtl91si4qz3.png)

2. Click on MetaDefender Endpoint tray icon, select "Recheck" or "Check applications security" depends on the agent version you are running. Wait few minutes and check again.

![](https://uploads.developerhub.io/prod/1yda/i21vmx2bi0k61iz7ivm61xasx71ufxn9f9gyu55gicugav6qysdxi6g790zepimd.png)

For Linux devices, to run a check, please navigate to My OPSWAT Central Management, **Inventory > Devices**, and select your device and run the action, **Compliance Check**.

If you already enabled the Firewall but the issue still occurs, please log into [**OPSWAT Portal**](https://my.opswat.com/) and open a support ticket with us. Please attach screenshots which proves that Firewall status is ON and version of the product installed to the ticket.
