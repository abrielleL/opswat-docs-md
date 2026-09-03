<!-- source: https://www.opswat.com/docs/filescan/faq/sandbox-technology -->

# Do you use sandbox technology?

Yes, but it's emulation and not virtualization-based. In general, our experience has taught us that virtualization-based technology is particularly important for forensic and full attack chain analysis targeting a very specific environment. Unfortunately, the downside of such in-depth analysis is speed (time to reporting is typically within 5-10 minutes), scaling challenges, high maintenance, having to restrict to a specific environment, evasion techniques fingerprinting the analysis environment, and a large resource overhead. Instead, we focus on a sophisticated set of lightweight emulation engines that implement adaptive threat analysis and have shown to yield better results at a fraction of cost.

**MetaDefender Aether** is a best-in-class emulation sandbox with a proven track record of detecting highly evasive stage one malware. See showcase reports [here.](https://www.opswat.com/docs/filescan/datasheet/file-analysis---deep-extraction)

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
