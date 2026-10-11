<!-- source: https://www.opswat.com/docs/fenddiode/resetting-your-diode/resetting-your-diode -->

# Resetting Your Diode

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Fend diodes include a physical reset button that can be used to perform a power cycle (reset) or return to factory settings (restore). This button is located to the left of the input side power jack and requires a small pin or paperclip to press.

**Power Cycle (Reset)** **– Quick press and release** – To power cycle the diode, perform a short press and release of the reset button. This will reboot both the input side and the output side. Use this feature if the diode is behaving unexpectedly or you need to reset a connection.

**Factory Settings (Restore) – Press, hold 10 seconds, and release** – To restore a diode to its original factory settings, press the reset button, hold for 10 seconds, and then release. After releasing, a green/yellow/red LED animation cycle will appear on LED Bank A of the input side to indicate a successful restore. See [**Appendix V: Status Indicator Light Patterns**](https://www.opswat.com/docs/fenddiode/appendices/appendix-v-status-indicator-light-patterns) “Factory Restore” for more details. This process is very quick and when done, both sides of the diode will reboot. **Factory restore will reset all configuration settings back to their defaults. This includes IP address, protocol selections,** **and even passwords!** Please use this feature if you have made a change to the diode and are no longer able to login to a configuration session.

After a factory reset, you will be able to connect to the diode at the default IP address of 192.168.1.99 and the original username/password that was sent with your unit.

**Special notice for diodes shipped with firmware versions 1.0.0 and 1.0.1** ***only*:** The factory restore feature was added with the 2.0.3 firmware release. Diodes that were shipped with a firmware version of 1.0.0 or 1.0.1 did not come with a factory restore point. The factory restore feature will not work until the diode’s firmware is upgraded to version 2.0.3 or above. When these diodes are upgraded, a factory restore point is created during the firmware upgrade process, as follows:

| Original Firmware | Upgrade Firmware | Factory Restore IP | Factory Restore Password |
| --- | --- | --- | --- |
| 1.0.0 or 1.0.1 | 2.0.3 | Input side IP address at time of FW upgrade | Password at time of FW upgrade |
| 1.0.0 or 1.0.1 | 2.1.0+ | Factory default IP (192.168.1.99) | Password at time of FW upgrade |

We recommend documenting your input side IP address and password before upgrading past 1.0.0/1.0.1 or changing the IP and password back to what was sent with your unit from the factory before upgrading.
