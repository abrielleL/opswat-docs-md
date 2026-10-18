<!-- source: https://www.opswat.com/docs/filescan/faq/java-21-notice-for-metadefender-aether--no-action-required -->

# Java 21 Notice for MetaDefender Aether: No Action Required

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Overview**

**What is it?**

MetaDefender Aether v3.3.0 added an in-product notice that a future release would need Java 21 in place of Java 17. Until now, the Aether engine has relied on a separately installed Java runtime that customers maintained. This was the only external dependency of the engine.

**Why was the notice added?**

Upcoming Aether features are built on a newer Java runtime. The notice gave customers early warning so they could plan for the change ahead of any upgrade requirement.

**Why is no action needed?**

Future releases of the Aether engine will include their own Java runtime, so a separate Java installation, upgrade or management is no longer required. From v3.3.1, the Java 21 notice no longer appears. Systems running Java 17 continue to work as they do now, and no Java upgrade is required.

**Frequently asked questions**

**Is a Java 21 installation required?**

No. The required runtime will ship with the engine.

**Are existing Java 17 installations still supported?**

Yes. Existing Java 17 installations continue to work and remain supported.

**What changes when the bundled runtime is released?**

The engine will use its own Java runtime, and the install package will be about 200 MB larger. After the upgrade to that release, the separately installed Java can be removed if no other application on the system uses it.

**Why was the notice removed in v3.3.1?**

The notice no longer applies. Java will ship with the engine, so no Java upgrade is required.

**When will the bundled runtime be available?**

In an upcoming release. The release notes for that version will confirm the details.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
