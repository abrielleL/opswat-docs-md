<!-- source: https://www.opswat.com/docs/mdss/4.5.2/where-to-get-help/unable-to-remove-docker-network -->

# Unable to remove docker network

If you encounter some message regarding your network:

**network mdss_stack id xxx has active endpoints**

while you tried to remove or update MDSS, please try to restart docker:

```bash
systemctl restart docker
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
