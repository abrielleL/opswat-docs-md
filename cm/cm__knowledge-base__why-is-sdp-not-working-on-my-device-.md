<!-- source: https://www.opswat.com/docs/cm/knowledge-base/why-is-sdp-not-working-on-my-device- -->

# Why is SDP not working on my device?

> **Info**
>
> This document will be updated periodically when environmental issues arise that can affect SDP from being used on your local device. If you believe to have an environmental issue that is not listed in this document, please reach out to OPSWAT support.

When enabling SDP for end-client devices, OPSWAT client will receive a command from My OPSWAT Central Management to install SDP. Sometimes, due to unforeseen environment variables, you may experience some issues connecting via SDP.

## Problem 1: Dell ExpressConnect/Dell Optimize is installed on your device.

My OPSWAT Central Management SDP is not compatible with Dell ExpressConnect/Dell Optimize. More information about the product [here](https://dl.dell.com/manuals/common/dell-emc-expressconnect-client-network-traffic-opt.pdf). Symptoms include:

- Ping or traceroute via ICMP successfully works.
- TCP traffic over the tunnel does not work.

**Solution**: Uninstall Dell ExpressConnect/Dell Optimize, and SDP will successfully connect.
