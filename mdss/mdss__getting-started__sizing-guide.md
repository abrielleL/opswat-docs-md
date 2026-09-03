<!-- source: https://www.opswat.com/docs/mdss/getting-started/sizing-guide -->

# Sizing Guide

This table summarizes the various deployment options available for MDSS. It helps you understand the differences between each option and choose the one that best fits your needs.

|  |  | Small scale deployments |  |
| --- | --- | --- | --- |
| **Feature** | **Basic Deployment (Single Instance)** | **Basic Deployment with Self-Hosted Shared Services** | **Basic Deployment with Managed Services** |
| **Best for** | *Small and predictable workloads* | *Small workloads, some flexibility, HA desired* | *Small workloads, with managed services* |
| **Scalability** | NO | NO | NO |
| **High Availability** | NO | NO | PARTIAL |
| **Auto-Scale Ready** | NO | NO | NO |
| **Files / hour** (Objects / hour) | **5,000** (125,000) | **20,000** (500,000) | **50,000** (1,250,000) |
| **Recommended MD Core** # | 2-4 | 4 or more | 4 or more |
| **Recommended MDSS #** | 1 | 1 | 1 |
| **Infrastructure complexity** | 1/5 | 4/5 | 3/5 |

|  | Medium scale deployments |  | Large scale deployments |  |
| --- | --- | --- | --- | --- |
| **Feature** | **Advanced Deployment with Self-Hosted Shared Services** | **Advanced Deployment with Managed Services** | **Cloud Deployment with Kubernetes (k8s)** | **MDSS Cloud (SaaS)​** |
| **Best for** | *Medium workloads, manual scaling* | *Medium to Large workloads, no auto-scaling* | *Large workloads, dynamic scaling, cost-optimized* | Scalable, secure, efficient cloud-based storage security solution |
| **Scalability** | YES | YES | YES | YES |
| **High Availability** | YES | YES | YES | YES |
| **Auto-Scale Ready** | NO | NO | YES | YES |
| **Files / hour** (Objects / hour) | **100,000** (2,500,000) | **100,000** (2,500,000) | **100,000** or more | **500,000** or more |
| **Recommended MD Core** # | 4 or more | 4 or more | Tailored per customer | Tailored per customer |
| **Recommended MDSS #** | 2 or more | 2 or more | Tailored per customer | Tailored per customer |
| **Infrastructure complexity** | 5/5 | 4/5 | 1/5 | 1/5 |

## [How we tested and what it means](/docs/mdss/getting-started/sizing-guide#how-we-tested-and-what-it-means)

We tested MDSS with a mix of everyday files, like documents, images, and videos, to get realistic performance numbers. We started small and then scaled up to see how it handled larger workloads. However, remember that these are just guidelines. Your actual performance will depend on your files, network, and hardware. For critical systems, it's always best to test it out yourself.

The numbers in the deployment table are based on rigorous testing using a diverse set of real-world files. We didn't just use one type of file; we included a mix of:

- **Documents** - PDFs, Word files (DOC/X), Excel files (XLS/X), PowerPoint files (PPT/X)
- **Executables** - EXEs, MSIs (installation files)
- **Images -** BMP, JPG, PNG
- **Media** - MP3, MP4 (audio and video)
- **Text and Archives** - various text files and compressed archives

#### [The Numbers Explained](/docs/mdss/getting-started/sizing-guide#the-numbers-explained)

- **our starting point was 5,000 files**, totaling 7,728.5 MB. The average file size was 1.55 MB.
- to see how MDSS handles **bigger workloads**, we replicated this dataset to create scenarios with 50,000 files and over 100,000 files. This helped us understand performance scaling.

The numbers in the table are meant to be *guidelines*. Real-world performance can vary due to:

- **File Type Variations** - some file types are processed faster than others.
- **Network Speed** - a slow network can impact throughput.
- **Hardware Specs** - the performance of your servers matters.

For mission-critical applications we strongly recommend running your own performance tests (benchmarks) in your specific environment *before* deploying MDSS in production. This will give you the most accurate picture of how MDSS will perform with your unique setup.
