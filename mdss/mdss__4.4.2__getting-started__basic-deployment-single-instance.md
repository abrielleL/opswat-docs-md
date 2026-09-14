<!-- source: https://www.opswat.com/docs/mdss/4.4.2/getting-started/basic-deployment-single-instance -->

# Basic Deployment

The basic deployment is the fastest way to get **MetaDefender Storage Security (MDSS)** up and running. All system components — MDSS, Metadefender Core, and shared services — are installed on a single machine.

Imagine running MDSS on a single computer. It's fast to set up and good for small tasks. But if you need to handle a lot of work or can't afford any downtime, this isn't the right choice.

#### [Suitable For](/docs/mdss/4.4.2/getting-started/basic-deployment-single-instance#suitable-for)

- Small workloads (perfect for testing or light usage)
- Quick setup with minimal configuration

#### [Key Points](/docs/mdss/4.4.2/getting-started/basic-deployment-single-instance#key-points)

- All components run on one server.
- You can't add more servers to handle more load.
- If the server goes down, MDSS goes down.
- You can still reconfigure or upgrade MDSS on this setup.

#### [Important Considerations](/docs/mdss/4.4.2/getting-started/basic-deployment-single-instance#important-considerations)

- Performance will vary depending on your server and file types.
- This setup is *not recommended* for live, critical systems where you need high availability or the ability to handle a lot of data.
- You get simplicity, but you lose the ability to scale and ensure continuous operation.
