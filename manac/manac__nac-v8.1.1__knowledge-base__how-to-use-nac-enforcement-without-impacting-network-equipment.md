<!-- source: https://www.opswat.com/docs/manac/nac-v8.1.1/knowledge-base/how-to-use-nac-enforcement-without-impacting-network-equipment -->

# How to use NAC enforcement without impacting network equipment?

This article applies to the current NAC Enforcer, the Web UI, and a range of supported network equipment.

To ensure that your network equipment (including routers, access points, controllers, switches, etc.) is not adversely impacted while using NAC, consider applying one of the following three options.

## [Option 1 (recommended)](/docs/manac/nac-v8.1.1/knowledge-base/how-to-use-nac-enforcement-without-impacting-network-equipment#option-1-recommended)

Under the **NAC Dashboard>Configuration>RADIUS>Device Authorization**, administrators can **Bulk Impor**t the MAC addresses of their network equipment into Authorized Devices, with a role configured with both a description of the equipment and a **Compliant** status. More details on this available [here](https://docs.opswat.com/manac/knowledge-base/how-to-use-authorized-devices).

## [Option 2](/docs/manac/nac-v8.1.1/knowledge-base/how-to-use-nac-enforcement-without-impacting-network-equipment#option-2)

This is for use in cases where Option 1, which is the recommended setup, is not viable, and the network equipment has an entirely reserved subnet.

Under the **NAC Dashboard>Policies>Qualifiers Menu>Qualifiers>Subnet**, administrators can create a new **Qualifier** for the subnet, then add that Qualifier into **Free Access**.

Support:

If you have further inquiries, concerns or issues **Using NAC Enforcement Without Impacting Network Equipment**, please open a [Support Case](https://my.opswat.com/portal/support) with the OPSWAT team via phone, online chat or form, or feel free to ask the community on our [OPSWAT Expert Forum](https://go2.opswat.com/s).
