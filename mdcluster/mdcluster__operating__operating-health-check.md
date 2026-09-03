<!-- source: https://www.opswat.com/docs/mdcluster/operating/operating-health-check -->

# Health check

The **Health Check** configuration page in OPSWAT MetaDefender Cluster allows administrators to define the minimum operational thresholds required for the system to be considered "**healthy**" and ready to process traffic from MD API Gateway for submitting files to scanning. By setting these parameters, you ensure that the system maintains your required baseline before accepting and scanning files.

### [Configuration Parameters](/docs/mdcluster/operating/operating-health-check#configuration-parameters)

- **Minimum number of active MetaDefender Core:** The minimum number of MD Core servers that must be healthy. (Minimum value: 1)
- **Minimum number of active AV engines:** The minimum total AV engines that must be operational across MD Core instances. (Minimum value: 1)
- **Required engines:** Specific mandatory engines (e.g., `FileType`, `Archive Extraction`, `AhnLab`) that **must** be active, regardless of the overall engine count.

### [System Behavior on Failure](/docs/mdcluster/operating/operating-health-check#system-behavior-on-failure)

If any of the above conditions are not met, MD Cluster is considered unhealthy. As a result, the **MD API Gateway will return an error** to the client if they attempt to submit a file for scanning.

Info

The MD API Gateway may receive a health status signal later than expected due to the polling intervals between scheduled health checks.
