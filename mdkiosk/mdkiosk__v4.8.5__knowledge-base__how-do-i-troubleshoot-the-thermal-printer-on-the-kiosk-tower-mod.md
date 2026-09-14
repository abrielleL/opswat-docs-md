<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-troubleshoot-the-thermal-printer-on-the-kiosk-tower-mod -->

# How do I troubleshoot the thermal printer on the Kiosk Tower model?

This article applies to the OPSWAT Kiosk Hardware K300x only

Kiosk Hardware K300x includes a built-in thermal printer. In some cases, you may encounter issues with the printer.

Before contacting OPSWAT Support, please try the following troubleshooting steps:

## [1. The printer makes repeated alarm sounds.](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-troubleshoot-the-thermal-printer-on-the-kiosk-tower-mod#1-the-printer-makes-repeated-alarm-sounds)

You will hear an alert sound from the built-in thermal printer when it runs out of paper. This sound indicates an out-of-paper status. To resolve this, follow the steps below:

- Open the printer compartment door located at the front center of the Kiosk.

- Press the Eject button to release and open the paper tray.

- Insert a new roll of thermal paper, or reposition the existing one correctly. Leave a small piece of paper outside the printer, as shown in the picture above.
- Close the paper tray.

## [The printer prints the blank paper](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-troubleshoot-the-thermal-printer-on-the-kiosk-tower-mod#the-printer-prints-the-blank-paper)

If the printer outputs blank paper, the roll may be loaded incorrectly. Thermal paper has only one printable side. Flip the roll so the correct side faces up. You can check by scratching the paper with your fingernail—if it leaves a black mark, that’s the side that should face up.

After switching the paper side, you can print a test page by following these steps:

- Press and hold the Power button to turn off the printer.
- Press and hold both the Power and Feed buttons together for 3 seconds, then release them.
- The printer will automatically print a test page.

## [3. The paper printed with blank stripes](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-troubleshoot-the-thermal-printer-on-the-kiosk-tower-mod#3-the-paper-printed-with-blank-stripes)

After extended use, the laser head surface may become contaminated, blocking the laser beam and causing blank stripes on the printouts. To fix this, follow these steps:

- Open the paper tray as instructed above.
- Gently clean the laser head—located beneath the front LED panel—using a soft brush or microfiber cloth.

- Insert the paper again and close the paper tray.
- Try to print the test page.

## [4. The printer doesn’t print, but the MD Kiosk shows that the printing is complete](/docs/mdkiosk/v4.8.5/knowledge-base/how-do-i-troubleshoot-the-thermal-printer-on-the-kiosk-tower-mod#4-the-printer-doesnt-print-but-the-md-kiosk-shows-that-the-printing-is-complete)

In this case, the current Windows default printer may not be set correctly. Follow the steps below to ensure the Kiosk printer is selected as the default printer:

- Close the Kiosk UI.
- Go to Control Panel> Hardware and Sound > Devices and Printers

- From the Printers list, find TP85. Right-click and choose “**Set as default printer**”

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chat with our support engineer**](https://my.opswat.com/support).
