<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/-linux--how-to-download-docker-images-from-alternate-location- -->

# [Linux] How to download docker images from alternate location?

If Docker Hub is inaccessible during installation, you can proceed with either an [Linux Offline Installation](https://www.opswat.com/docs/mdss/installation/linux-offline-installation) or by specifying an alternative container registry. To configure an alternate registry, add the necessary details to the `customer.env` file.

```bash
MDSS_REPO=public.ecr.aws/v2f5u9p9/opswat-mdss
POSTGRES_IMAGE=public.ecr.aws/v2f5u9p9/opswat-mdss/postgres
RABBITMQ_IMAGE=public.ecr.aws/v2f5u9p9/opswat-mdss/rabbitmq
REDIS_IMAGE=public.ecr.aws/v2f5u9p9/opswat-mdss/garnet-alpine
```

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
