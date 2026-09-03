<!-- source: https://www.opswat.com/docs/manac/knowledge-base/policy-key-reporting-behavior -->

# Policy Key Reporting Behavior

## [How often do Policy Key devices report to the NAC server?](/docs/manac/knowledge-base/policy-key-reporting-behavior#how-often-do-policy-key-devices-report-to-the-nac-server)

Each Policy Key (PK) instance periodically reports its compliance status to the MetaDefender NAC server.

This reporting interval—sometimes referred to as the **"scan interval"**—defines how often the NAC tells PK instances to wait between reports, and how long the NAC expects to hear from each PK instance under normal conditions.

> **Note:** The Policy Key checks compliance policies **locally** more frequently than this, but only reports to the NAC according to the scan interval unless there is a compliance status change (see below).

---

## [How the reporting interval is calculated](/docs/manac/knowledge-base/policy-key-reporting-behavior#how-the-reporting-interval-is-calculated)

The reporting interval is determined based on the number of devices currently online.\

The NAC dynamically adjusts this interval to balance the need for real-time compliance data against the risk of having PK instances on large networks unintentially DDoS it. The formula used is:

reporting_interval_sec = max(
online_device_count / target_requests_per_sec,
min_contact_out_compliance
)

- **online_device_count** — Number of endpoints currently connected to the network
- **target_requests_per_sec** — Number of Policy Key reports the NAC would like to handle per second *(default: 5 requests per second)*
- **min_contact_out_compliance** — Minimum time between reports, even on small networks *(default: 300 seconds / 5 minutes)*

**Example:**

If there are 5,000 active devices on a medium-sized network:

reporting_interval_sec = max(5000 / 5, 300)
= max(1000, 300)
= 1000 seconds (~16.7 minutes)

---

## [When a device becomes non-compliant](/docs/manac/knowledge-base/policy-key-reporting-behavior#when-a-device-becomes-non-compliant)

If a Policy Key device fails to report within **twice** its reporting interval, the NAC assumes it no longer has the PK installed or running. If policy settings require the device to have the PK, it will be **blocked and redirected** to the PK download page.

timeout_time_sec = 2 * reporting_interval_sec

Using the same example:

timeout_time_sec = 2 * 1000
= 2000 seconds (~33 minutes)

In this case, a device would be blocked after about **30 minutes** of no contact.

---

## [Immediate reports on compliance changes](/docs/manac/knowledge-base/policy-key-reporting-behavior#immediate-reports-on-compliance-changes)

If a Policy Key detects a compliance change—such as an antivirus becoming out of date, a missing patch being installed, or a policy violation being resolved—it **immediately reports** this to the NAC, ignoring the normal reporting interval. This ensures the NAC always has up-to-date compliance information.

---

## [Adjusting these settings](/docs/manac/knowledge-base/policy-key-reporting-behavior#adjusting-these-settings)

The reporting and timeout intervals use sensible defaults that work for most environments, but they can be tuned if your deployment has specific performance or responsiveness needs.

If you’d like to adjust these defaults, please **contact OPSWAT Support** for assistance.
