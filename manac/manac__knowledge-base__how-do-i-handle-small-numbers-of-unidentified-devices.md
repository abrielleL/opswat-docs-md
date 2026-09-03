<!-- source: https://www.opswat.com/docs/manac/knowledge-base/how-do-i-handle-small-numbers-of-unidentified-devices -->

[NAC](https://www.opswat.com/docs/manac)Need Help?
# How do I handle a small number of unidentified devices?

- **MAC Address** - gather the device’s MAC address. This can be done through the Device Manager if you know the endpoint’s current IP address. Otherwise you can gather it directly from the network settings on the device in question.
- **Identity** - If possible, a staffer should view the device directly so as to confirm the reported make/model and device type. If necessary, you can gather this information from trusted end users.
- **Exemption** - Place the device in Open Access by MAC address in the Device Manager. Set the expiration date out far enough that the new fingerprint can be created and propagated before the device reverts to normal policy. Typically this should be 10 days or so.

Support:

If Further Assistance is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
