<!-- source: https://www.opswat.com/docs/mdss/4.5.2/getting-started/basic-deployment-single-instance -->

# Basic Deployment

The basic deployment is the fastest way to get **MetaDefender Storage Security (MDSS)** up and running. All system components — MDSS, Metadefender Core, and shared services — are installed on a single machine.

Imagine running MDSS on a single computer.  It's fast to set up and good for small tasks.  But if you need to handle a lot of work or can't afford any downtime, this isn't the right choice.

![](https://uploads.developerhub.io/prod/k8zL/hm0qcel164za14ye4zt1ada9nocknic9qdsa26dq86ns90jnydp1alo4sczua2yt.png)

#### Suitable For

- Small workloads (perfect for testing or light usage)
- Quick setup with minimal configuration

#### Key Points

- All components run on one server.
- You can't add more servers to handle more load.
- If the server goes down, MDSS goes down.
- You can still reconfigure or upgrade MDSS on this setup.

#### Important Considerations

- Performance will vary depending on your server and file types.
- This setup is *not recommended* for live, critical systems where you need high availability or the ability to handle a lot of data.
- You get simplicity, but you lose the ability to scale and ensure continuous operation.

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
