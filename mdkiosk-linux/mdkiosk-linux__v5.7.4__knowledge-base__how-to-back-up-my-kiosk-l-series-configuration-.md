<!-- source: https://www.opswat.com/docs/mdkiosk-linux/v5.7.4/knowledge-base/how-to-back-up-my-kiosk-l-series-configuration- -->

# How to back up my Kiosk L-Series configuration?

This article applies to all MD Kiosk L-Series that are managed in My OPSWAT

MD Kiosk L-Series is one of the advanced products that limits almost all setting modifications. While using this product, sometimes, you will have to reset the Kiosk, which will erase the current configurations, but the product itself doesn’t have a backup/restore feature like other products.

To resolve the need, we can utilize the Group Setting feature on the Central Management to back up the configuration. Then, the next time you connect the Kiosk back to the Central Management, you can apply the Group Setting to the Kiosk to restore the configuration.

**BACKUP:**

1. Browse to the instance configuration: Central Management > Products > MetaDefender Kiosk L-Series > Instances > Choose the instance > Configuration

2. Finalize the Kiosk settings, then click on Set as Group configuration and confirm the change.

**RESTORE:**

1. After connecting the Kiosk to the Central Management, make sure that the Kiosk is assigned to the right group.
2. Browse to Groups management: Central Management > Products > MetaDefender Kiosk L-Series > Groups > Choose the Group

3. Choose the instance that you want to restore the configuration, and browse to Actions > Apply group configuration.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
