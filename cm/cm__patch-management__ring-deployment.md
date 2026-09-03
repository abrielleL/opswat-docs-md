<!-- source: https://www.opswat.com/docs/cm/patch-management/ring-deployment -->

# Ring Deployment

Ring Deployment rolls out patches in stages instead of pushing them to every device at once. Patches go to a small group first and only move forward once enough devices in that group install them successfully. Use it to reduce risk when patching large or sensitive environments.

![](https://uploads.developerhub.io/prod/97qW/d46btcang07whyhrm261lc4g73jkooqjsnntqzim9vrn9pch1upu9zq600m3rchl.jpg)

## Related Topics

Use the following guides to understand the Ring Deployment workflow and create your staged rollout:

- [How Ring Deployment Works](https://www.opswat.com/docs/cm/patch-management/how-ring-deployment-works)
- [Create Ring Deployment](https://www.opswat.com/docs/cm/patch-management/create-ring-deployment)

## When To Use Ring Deployment

Choose a ring deployment when the risk of a bad patch reaching every device at once is too high to accept, typically on large fleets or with high-impact patches. Use a standard deployment for known-safe patches, urgent fixes, and smaller fleets. The table below compares both modes at a glance.

|  | Standard deployment | Ring deployment |
| ---- | ---- | ---- |
| **Rollout** | All devices at once | Sequential waves, ring by ring |
| **Risk control** | All-or-nothing, a bad patch reaches everyone | Blast radius contained to each ring until promotion |
| **Promotion** | N/A | Automatic or manual, evaluated per patch |
| **Reusability** | One-off (on-demand) or recurring (policy) | Reusable configuration, creates a new run on each schedule |
| **Best for** | Known-safe patches, urgent fixes, smaller fleets | Large fleets, high-risk patches, compliance-sensitive environments |

##
