<!-- source: https://www.opswat.com/docs/product-management/knowledge-base/a-product-instance-s-configuration-not-loaded -->

# A product instance is in Pending status and could not load its configuration

| Term | Details |
| --- | --- |
| Problem | The product instance has been in Pending status for a long time.  The product instance could not load its configuration and shows the error "The instance has not fully reported its configuration". |
| Cause | The product instance has not fully submitted its configuration to My OPSWAT. This can happen when the instance enrolled to My OPSWAT before My OPSWAT supports configuration management feature for the product or the product is running a version that has not supported that feature. |
| Troubleshooting | Check the product version and if the instances were enrolled before the product's configuration management feature was supported. |
| Solution | Upgrade the product to a version that supports configuration on My OPSWAT if needed. |

A product instance stays at Pending status for a long time and when you open its configuration page, the error "The instance has not fully reported its configuration" is shown like in the image below.

The product instance has not submitted its configuration upon the instance's enrollment.

Please make sure that you are running a product version that supports configuration on My OPSWAT. If not, please upgrade the product to a minimum version that listed [here](/docs/product-management/operating/product-dashboard).

If the product already runs a version that supports configuration on My OPSWAT and the issue still persists, it seems like the product enrolled or upgraded please before you upgrade My OPSWAT to a version that supports configuration management feature for the product. Please unenroll and enroll the product instance again.

Please contact OPSWAT Support so our team can help you remediate this issue.
