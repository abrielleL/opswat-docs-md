<!-- source: https://www.opswat.com/docs/mdkiosk/v4.8.5/knowledge-base/which-kiosk-hardware-model-am-i-using- -->

# Which Kiosk Hardware Model am I using?

This article applies to OPSWAT Kiosk Hardware only.

Kiosk hardware comes in multiple variants. The actual hardware models may vary over time. The list below shows the vendor hardware models associated with each kiosk hardware name.

| **Kiosk Category** | **Hardware Model** | **Vendor Hardware Model** |
| --- | --- | --- |
| Kiosk Tower (K3XXX) | K3000 (Obsoleted) | OptiPlex 5060 Small Form Factor |
|  | K3001 | OptiPlex 7000 (D17S) |
|  |  | OptiPlex 7090 (D15S) (D17S) |
|  |  | OptiPlex XE4 (D17S) |
|  | K3001-CB | OptiPlex XE4 (D17S) |
| Kiosk Mobile (K2XXX) | K2001 (Obsoleted) | Surface Pro 7 |
|  | K2100 | Dell 7220 |
|  |  | Dell 7230 |
| Kiosk Desktop (K1XXX) | K1000 (Obsoleted) | Lenovo M820z |
|  | K1001 | Lenovo M70a (End of Sale) |
|  |  | Dell 7410 |
|  |  | Dell 7420 |
| Kiosk Mini | Kiosk Mini | Dell 7230 |
| Kiosk L100x | L1001 | Lenovo M70a (End of Sale) |
|  |  | Dell 7410 |
|  |  | Dell 7420 |

**How do we verify the Vendor hardware model?**

To verify the vendor hardware model, use the serial number (Service Tag for Dell) and check the warranty lookup page for complete hardware details.

Lenovo: [Lenovo Warranty Check | Device Warranty Lookup | Lenovo Support US](https://pcsupport.lenovo.com/us/en/warranty-lookup#/)

Dell: [Support Services & Warranty | Dell US](https://www.dell.com/support/contractservices/en-us)

Below are some methods to get the Serial Number (ServiceTag):

- Using CMD: **wmic bios get serialnumber**

- Locate the manufacturer’s label and check for the Serial Number (Service Tag - Dell). Dell 7410:

Especially with K3001, you need to verify whether the Reg Model is D15S or D17S

Lenovo M70a:

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
