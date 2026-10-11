<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on -->

# Kiosk Desktop: Black screen for about 15 seconds after power-on

View as Markdown Ask ChatGPT about this page Ask Claude about this page
# [**1. Summary**](/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on#1-summary)

When you press the power button on the Kiosk Desktop (Dell Pro 24 AIO), the power button lights up, but **nothing appears on the screen for about 15 seconds**. The screen stays black during this time, so the computer can look like it isn't responding or has a problem.

**This is expected behavior for this model. The device is working normally.** After about 15 seconds, the Dell logo appears and the computer continues to start up as usual.

Wait at least 15 seconds after pressing the power button before deciding that something is wrong.

# [**2. Why this happens**](/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on#2-why-this-happens)

Before anything can appear on screen, the computer runs startup checks:

• prepares the memory

• checks the processor and system board

• verifies the BIOS firmware and security chip

**By default, a computer cannot display anything on the screen until these checks finish.** This applies to all computers, not only the Kiosk Desktop.

Some devices show the Dell logo as soon as you press the power button. These devices use a BIOS feature called **Early Logo Display** (under **Sign of Life**). It shows the logo straight away while the startup checks continue in the background.

Not all devices support this feature. **Most Dell desktop and All-in-One models, including the Dell Pro 24 All-in-One used in the Kiosk Desktop, do not support Early Logo Display.** On these models, the screen stays black until the startup checks finish, which takes about 15 seconds. The computer is working normally during this time.

# [**3. Correct power-on process**](/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on#3-correct-power-on-process)

| Step | What you do | What you see |
| --- | --- | --- |
| 1 | Press the power button (bottom edge of the computer)  once and release it. | The power button lights up. |
| 2 | Wait. Do not press any button. | The screen stays black for about 15 seconds.  This is normal. |
| 3 | Keep waiting. | The Dell logo appears. |
| 4 | Keep waiting. | Windows (or your application) loads. |

**Important: do not press or hold the power button again while the screen is black.**

- Pressing it again can put the computer to sleep or interrupt startup.
- Holding it for **10 seconds** forces the computer to shut down.

# [**4. Troubleshooting: if startup does not go as described**](/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on#4-troubleshooting-if-startup-does-not-go-as-described)

***A. The power button does NOT light up***

1. Check that the power cable is firmly connected to the computer and the wall outlet.
2. Try a different wall outlet.
3. Check the **power-supply diagnostics light** on the back panel:

   1. **Light on:** the computer is receiving power. Go to step 4.
   2. **Light off:** the power cable, wall outlet or power supply may be faulty. Try another power cable if available, then contact support.
4. **Drain residual power:**

   1. Unplug **all cables** connected to the computer: the power cable, network (Ethernet) cable, USB devices and any other connected cables.
   2. Press and hold the power button for 15 seconds.
   3. Reconnect the power cable only.
   4. Press the power button once and wait at least 15 seconds.
   5. If the computer starts, reconnect the other cables.
5. If the power button still does not light up, contact support.

***B. The power button is lit, but the screen stays black for more than 1 minute***

1. **Wait the full minute.** The first start after a BIOS update, a hardware change or a power loss can take longer than usual.
2. **Check whether the power button is blinking amber/white.** If it is, the computer is showing a diagnostic error code. Count the **amber** blinks, then the **white** blinks, note the pattern, and contact support.

| Amber, White | Problem |
| --- | --- |
| 1, 1 | TPM detection failure |
| 1, 2 | SPI flash failure |
| 2, 1 | CPU failure |
| 2, 2 | System board failure / BIOS corruption |
| 2, 3 | No memory detected |
| 2, 4 | Memory failure |
| 2, 5 | Invalid memory installed |
| 2, 6 | System board / chipset error |
| 2, 7 / 2, 8 | LCD failure |
| 3, 1 | CMOS battery failure |
| 3, 2 | Video chip failure |
| 3, 3 / 3, 4 | BIOS recovery image not found / invalid |
| 3, 5 | Power rail failure |
| 3, 6 | Flash corruption |
| 3, 7 | Intel ME timeout |

3. Shut down by holding the power button for 10 seconds.
4. **Drain residual power** as in section A, step 4.
5. Contact support.

***Optional: label for the device***

**Power on: press the button ONCE, then wait about 15 seconds.**

The screen stays dark while the computer starts (the power light indicator is on). This is normal. Do not press the button again.

15 seconds after power-on](https://www.opswat.com/docs/mdkiosk/v4.8.6/knowledge-base/kiosk-desktop--black-screen-for-about-15-seconds-after-power-on#)
