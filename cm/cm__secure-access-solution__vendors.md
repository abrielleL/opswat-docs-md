<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/vendors -->

# Vendors

Vendors are key to RADIUS NAC, helping to identify and assign the right access profiles for new devices joining the network. Administrators can easily customize vendors to fit their organization’s specific needs.

### Create Vendor

To create a new Vendor,

1. Log into the **My OPSWAT Central Management** console as Administrator
2. Navigate to **RADIUS NAC ->** **Vendors**
3. Click on **Add Custom Vendor** button
4. Fill in the detailed information:
   1. Vendor Name
   2. Type: Wired or Wireless connection
   3. Mode: Dynamic Authorization mode in CoA (Change of *Authorization)*  or Disconnect
   4. Attribute and Value sets for sending CoA/Disconnect
5. Click on Save button

![](https://uploads.developerhub.io/prod/6Ad9/q97qvigx060va8ofoanuic1qlqz2gvwin4film60b1wvd3bgxgjkcz78qi3rsddm.png)

After a Vendor is created successfully, you can see the Vendor display for selection when create/update Access Profile

![](https://uploads.developerhub.io/prod/6Ad9/141bm7jan1xa0gdn1q9h1rjgswwafz4xopzrrahu11ymvwhqi4fgzdltn2pczrmh.png)

### Create Vendor with Specific Attributes

When creating an Access Profile, you may notice that some RADIUS Vendor attributes aren't available for selection, such as **Extreme-User-Vlan** for Aerohive or **Juniper-Local-User-Name** for Juniper.

![](https://uploads.developerhub.io/prod/6Ad9/nd277otyji0lvtolacnimkszabwtrkixaul2bu992h88kppyipupsg8doh3rkpr3.png)

![](https://uploads.developerhub.io/prod/6Ad9/qw9sefyw3jgqg03zpo34o4pbdfwaf38uf6kzy6a89kf10hm9f8psf6mhqm8ed4ci.png)

This happens because Vendor-Specific Attributes (VSAs) have not yet been enabled for the Vendor. To enable Vendor-Specific Attributes (VSAs) for a particular vendor, follow these steps:

1. Navigate to the **Vendor** tab
2. Select your specific vendor
3. Enable Vendor-Specific Attributes checkbox
4. Fill in your Vendor name (If your desired vendor is not listed, please reach out to OPSWAT support for assistance).
5. Click on Save
