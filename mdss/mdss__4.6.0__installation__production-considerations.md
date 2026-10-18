<!-- source: https://www.opswat.com/docs/mdss/4.6.0/installation/production-considerations -->

# Production Considerations

This section of the user guide focuses on essential production considerations. When deploying in a production environment, it is recommended to follow this guide to ensure optimal security and reliability. Key steps include:

1. **Setting up HTTPS**: Ensure that HTTPS is configured to secure communication between clients and servers.
2. **Using an External Database**: Instead of the built-in database, configure an external database to handle your data for better performance and scalability.
3. **OS-Specific Tasks**: Perform operating system-specific tasks that enhance the security and reliability of your system.
4. **Planning for High Availability**: Add redundancy with an [active-active deployment](https://www.opswat.com/docs/mdss/configuration/active-active-configuration), or use the reference [active-passive failover script](https://github.com/OPSWAT/mdss-active-passive-failover), which monitors an active instance and, when it stops responding, starts a real-time scan of one chosen storage on a standby instance. Its usage is documented in its README.

Following these guidelines will help you maintain a secure and efficient production environment.

Depending on your deployment type, please choose between:

- [Production considerations for Unix-based deployments](https://www.opswat.com/docs/mdss/installation/linux-deployments)
- [Production considerations for Windows-based deployments](https://www.opswat.com/docs/mdss/installation/windows-deployments)

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
