<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/dhcp-infoblox -->

# How to send DHCP Syslog from Infoblox to NAC

1. From you Infoblox Dashboard click **System**  -> **System Properties**

![](https://uploads.developerhub.io/prod/97qW/sgw9l7g9g4xx07le9fph7yvp5ydmv463gh330tvfhboo5pmxtzaephfyu5wj7p0x.png)

2. Choose **Monitoring**

![](https://uploads.developerhub.io/prod/97qW/6bmtxmpelm60cgidoyl3ulpgzcfiiqxxoqvkmp4wwkl55am8sycyazfudcx82yro.png)

3. Configure as follows:
   1. **Log to External Syslog Servers:** Checked
   2. **Address:** [IP address of NAC Edge VM]
   3. **Port:** 514
   4. **Logging Category**: DHCP Process

![](https://uploads.developerhub.io/prod/97qW/w94j6m63qt5xn5d1g42crr1cr5shl8g2uo85vlrm6oh1cp4jmwk19odbf0vycdxe.png)

![](https://uploads.developerhub.io/prod/97qW/xu78en94wrzhlbbzlu0hhu9h0ezgnbrczr00oyf2ltu6si84p2tnjvotn3xwjsiw.png)
