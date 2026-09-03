<!-- source: https://www.opswat.com/docs/cm/secure-access-solution/nac-policy-logic--v8-vs--v10 -->

# NAC Policy Logic: v8 vs. v10

This document provides a detailed comparison of the policy and access control models in MetaDefender NAC v8 and MetaDefender NAC v10. It is intended to help administrators understand how v8 concepts map to v10, and where the models diverge.

---

## NAC v8 Policy Model

In v8, a device's network access is determined by three interrelated systems: **Policy Groups**, **compliance evaluation**, and **Role assignment**.

### Policy Groups

A Policy Group is a pairing of a **Qualifier Container** (who does this group apply to?) and a **Policy Container** (what must those devices comply with?).

For every device the NAC tracks on the network, the system walks the list of Policy Groups from top to bottom and matches the device to the first group whose Qualifier Container matches. The device is then said to "qualify into" that Policy Group.

### Qualifier Containers and Qualifier Sets

A Qualifier Container is a collection of **Qualifier Sets**. Each Qualifier Set is a collection of individual qualifiers of a uniform type:

- **Network** (e.g., subnet matches)
- **Host Type** (e.g., Windows, macOS, printer)
- **Identity** (e.g., user or group membership)
- **Device** (e.g., specific MAC addresses)

The matching logic is:

- **Within a Qualifier Set**: **OR** logic. A device only needs to match one qualifier in the set. For example, a Network set containing three subnets matches any device with an IP on any one of those subnets.
- **Between Qualifier Sets in a Container**: **AND** logic. A device must match all sets in the container. For example, a container with a Network set and a Host Type set requires a device to match at least one entry in each set.

> **Edge case:** If a Qualifier Container includes multiple Qualifier Sets of the same type, **OR** logic is applied between those same-type sets (rather than the usual AND). This is rare in practice.

### Policy Containers (Compliance)

A Policy Container is a list of policies that define compliance requirements — for example, "device must be authenticated," "device must have the Policy Key installed," or "device must have antivirus running." A device must pass **all** policies in its Policy Group's Policy Container to be considered compliant.

### Roles and the Role Matrix

The actual network access a device receives is determined by its assigned **Role**. Role assignment is controlled by a matrix defined under "RADIUS Configuration > Groups > Policy group mappings" with:

- A **row** for each Policy Group (plus a catch-all "All other groups" row at the bottom)
- Two **columns**: Compliant and Non-Compliant
- Each **cell** specifying a Role

A Role is a collection of RADIUS attributes (organized by vendor) to be included in Access-Accept packets sent to the switch, WLC, or AP (collectively “Network Access Server” or “NAS”) after RADIUS authentication (802.1x or MAB). These attributes may specify a VLAN, ACL, QoS policy, or other vendor-specific directives controlling network access.

The specific attributes sent to a given NAS for a given endpoint device depend on both the **Role** of endpoint device, and the **vendor** mapped to the NAS from which the Access-Request originated.

### Why Is It This Way?

This multi-layered structure exists for largely historical reasons. MetaDefender NAC v8 (formerly SafeConnect) was originally built for Layer 3 / Policy-Based Routing integrations, where network access is binary: a device's IP is either added to a block ACL or it isn't.

With Layer 2 / RADIUS-based integrations, network access becomes multi-dimensional — there are many possible access levels for "allowed" devices, and sometimes multiple levels of "blocked." Rather than rewriting the core business logic, support for RADIUS-based access was grafted onto the existing v8 qualifier/policy model using the Role Matrix described above.

---

## NAC v10 Policy Model

MetaDefender NAC v10 was designed from the ground up with RADIUS-based, role-based access control in mind. The model is significantly simpler, built around two key abstractions: **Rules** and **Access Profiles**.

### Access Profiles

An Access Profile is functionally identical to a v8 Role — a named collection of RADIUS attributes (organized by vendor) that define the network access a device should receive. The name was changed because "Role" is an overloaded term across IT systems.

### Rules

A Rule is a named set of **conditions** paired with an **Access Profile**. When a device authenticates against the v10 RADIUS server, the system walks the list of Rules from top to bottom and applies the first match — just like Policy Group qualification in v8. However, there are key differences:

1. **Direct access assignment.**
   1. In v8, qualifying into a Policy Group is only the first step — the system must then evaluate compliance and look up the appropriate Role in the matrix.
   2. In v10, a Rule match directly assigns the associated Access Profile. There is no separate compliance evaluation step or lookup matrix.
2. **Flexible condition logic.**
   1. In v8, qualifier matching follows a rigid hierarchy: qualifiers are grouped into typed Qualifier Sets (OR within a set), which are grouped into Qualifier Containers (AND between sets).
   2. In v10, conditions can be grouped into arbitrary collections with configurable AND/OR logic, and these collections can be nested to arbitrary depth.
3. **Compliance as a condition, not a separate system.** In v10, "device compliance status" and "device authentication status" are simply conditions you can include (or not) in your Rules — alongside network, identity, device type, or any other condition. Defining the security posture/compliance requirements of a device is handled by [MetaDefender Endpoint Policies](https://www.opswat.com/docs/cm/product-management/metadefender-endpoint-policies).

---

## Concept Mapping

The table below maps v8 concepts to their closest v10 equivalents, but note that the relationship is not always one-to-one due to the architectural differences described above.

| **NAC v8 Concept** | **NAC v8 Concept** | **Notes** |
| ---- | ---- | ---- |
| Policy Group | Rule | Both use first-match, top-down evaluation. In v10, a Rule match directly assigns access rather than feeding into a compliance check + matrix lookup. |
| Qualifier Sets / Containers | Rule Conditions | v10 conditions support arbitrary AND/OR nesting rather than the fixed set/container hierarchy. |
| Policy Container | Rule Conditions | Compliance is a condition within Rules in v10, not a separate evaluation layer. |
| Role | Access Profile | Functionally identical; renamed to avoid term overloading. |
| Role Matrix | *(no equivalent)* | Unnecessary in v10 — Rules map directly to Access Profiles without an intermediary lookup. |
