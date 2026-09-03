<!-- source: https://www.opswat.com/docs/mdicap/getting-started/sizing-guide -->

# Sizing Guide

### [Sizing Guide](/docs/mdicap/getting-started/sizing-guide#sizing-guide)

This table summarizes the various deployment options available for MetaDefender ICAP Server to illustrate the differences between each option and choose the one that best fits your needs.

|  | Single Instance (Standalone) | Single Instance (Remote DB) | Multi-Instance (Standalone) | Multi-Instance (Remote DB) |
| --- | --- | --- | --- | --- |
| **Best for** | ***Small*** *and predictable workloads.*  ***On-premises, CSPs or Docker*** | ***Small*** *workloads, with managed services.*  **On-premises, CSPs or Docker** | ***Medium*** *workloads, manual scaling.*  _ _  ***CSPs or Kubernetes*** | ***Medium*** *to* ***Large*** *workloads, no auto-scaling.*  **CSPs or Kubernetes** |
| **Scalability** | NO | NO | YES | YES |
| **High Availability** | NO | PARTIAL | YES | YES |
| **Auto-Scale Ready** | NO | NO | NO | YES |
| **Recommended MD Cores** | 2-4 | 4 or more | 4 or more | 4 or more |
| **Recommended ICAP Servers** | 1-2 | 2-4 | 2 or more | 2 or more |
| **Infrastructure complexity** | 1/5 | 3/5 | 5/5 | 4/5 |

ICAP Server sizing recommendations

Overall performance and file throughput of the solution will depend on a variety of factors. When sizing your deployment, first consider the sizing requirements for MetaDefender Core. When adequately provisioned, ICAP Server can support the file traffic for up to (3) MetaDefender Core instances. In most cases, a ratio of (1) ICAP Server for every (2) MD Core servers is the best balance of performance, throughput and capacity.

This table describes a subset of the configuration and sizing options for MetaDefender ICAP Server. If more detailed technical sizing is required, please contact your sales engineer or representative.

Info

- The raw ICAP capacity is useful for cases when MetaDefender Core is going to be deployed to a separate server.

** The ICAP + Core capacity is useful for cases when MetaDefender Core is going to be deployed to the same server as MetaDefender ICAP Server.

## [Sizing Examples](/docs/mdicap/getting-started/sizing-guide#sizing-examples)

| Metric | Value | Value |
| --- | --- | --- |
| Number of simultaneous users (threads) | 10 | 100 |
| Data throughput (kB/s) | 8005 | 8070 |
| Request throughput (req/s) | 97.91280654 | 97.31414474 |
| Total requests | 35934 | 355002 |
| Total time | 367 | 3648 |
| CPU Cores | 2` | 8 |
| RAM | 8 GB | 16 GB |

### [Load values with 10 threads (left) / 100 threads (right)](/docs/mdicap/getting-started/sizing-guide#load-values-with-10-threads-left--100-threads-right)

### [Load Chart with 10 threads (left) / 100 threads (right)](/docs/mdicap/getting-started/sizing-guide#load-chart-with-10-threads-left--100-threads-right)

Measurement Methodology

1. MetaDefender Core connection was disabled to eliminate potential bottleneck caused by Core
2. 100 ms delay was applied between requests
3. Each user (thread) requested the whole dataset 10 times
4. Files were requested in a randomized fashion
## [Test Environment](/docs/mdicap/getting-started/sizing-guide#test-environment)

## [Traffic Mix](/docs/mdicap/getting-started/sizing-guide#traffic-mix)

| File Type | Percentage of traffic |
| --- | --- |
| Archive (zip) | 2.8% |
| Image | 2.5% |
| Microsoft Office | 10.7% |
| PDF | 1.5% |
| Windows executable (exe) | 24.2% |
| HTML | 19.6% |
| Text | 37.3% |
| Total | 98.6% |
| Rounding error | 1.4% |
