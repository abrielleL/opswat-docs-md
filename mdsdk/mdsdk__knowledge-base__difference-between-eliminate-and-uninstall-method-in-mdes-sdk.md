<!-- source: https://www.opswat.com/docs/mdsdk/knowledge-base/difference-between-eliminate-and-uninstall-method-in-mdes-sdk -->

# Differences between Eliminate and Uninstall method

This article is applied to MetaDefender Endpoint Security SDK releases deployed on Windows, MacOS.

## [**Overview**](/docs/mdsdk/knowledge-base/difference-between-eliminate-and-uninstall-method-in-mdes-sdk#overview)

When removing application software software using the MetaDefender Endpoint Security SDK, we offered two methods on our [official documentation](https://software.opswat.com/OESIS_V4/html/c_method.html): `Uninstall` and `Eliminate`. While both aim to remove a product from the system, they differ in how they work and when they should be used.

---

## [Uninstall method](/docs/mdsdk/knowledge-base/difference-between-eliminate-and-uninstall-method-in-mdes-sdk#uninstall-method)

The `Uninstall` method is the **official, supported**, and **recommended** way to remove applications.

- It works with products that are **recognized and supported** by OPSWAT’s database.
- It uses the product’s **standard uninstall process** to safely remove it from the system.
- It is **reliable** and tested for production use.

## [Eliminate method](/docs/mdsdk/knowledge-base/difference-between-eliminate-and-uninstall-method-in-mdes-sdk#eliminate-method)

The `Eliminate` method was designed to remove products, including those not officially supported. However, it is **not reliable for production** and has been **marked for deprecation**.

- It internally calls the `Uninstall` method, then attempts additional steps if needed.
- It may target unsupported or unknown products, which increases the chance of incorrect or incomplete removals.
- Due to quality concerns, it should **not be used in production environments**.

Recommendation

Use only the `Uninstall` method for removing software in your production environment. The Eliminate method will be **deprecated** soon from SDK.

Support

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
