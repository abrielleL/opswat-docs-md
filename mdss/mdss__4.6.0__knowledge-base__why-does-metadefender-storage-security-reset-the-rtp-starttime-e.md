<!-- source: https://www.opswat.com/docs/mdss/4.6.0/knowledge-base/why-does-metadefender-storage-security-reset-the-rtp-starttime-e -->

# Why does MetaDefender Storage Security reset the RTP StartTime every day?

> **Check Your Version:**
>
> This article applies to all MetaDefender Storage Security v4.2.0 deployed on Windows and Linux systems.

**Issue:** MetaDefender Storage Security resets the Real-Time Processing (RTP) Start Time every day.

![](https://uploads.developerhub.io/prod/k8zL/m63z4w5kcc1tju0djoo4eavbqlkon1tbclnbdosya6jr4if56ggwsxxbgh2adlj6.png)

**Resolution:** The reason for this behavior is enabling “Enable RTP history retention” under **Settings > Data Retention**.

This issue will be fixed in version 4.4.0.

**Workaround:** Currently, the workaround is to disable “Enable RTP history retention.”

![](https://uploads.developerhub.io/prod/k8zL/te3r093paq82tggeg3n3inqu4jmo7bari7xlnt27s83fqvx925j1so8h504qngm2.png)

> **Support:**
>
> If **Further Assistance** is required, please proceed to log a [support case or chatting with our support engineer](https://my.opswat.com/support).

---

[All pages in this documentation](https://www.opswat.com/docs/mdss/llms.txt)
