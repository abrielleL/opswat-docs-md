<!-- source: https://www.opswat.com/docs/supply-chain/operating/cryptography -->

# Cryptography

> **Prerequisite**
>
> Cryptography analysis needs MetaDefender Core 5.23.0 or later with the SBOM engine 5.0.0 or later. With an older version, the job shows **SBOM engine does not support CBOM** and no cryptographic assets.

The **Cryptography** tab of the Reports page is the asset-centric view of your scan results: every cryptographic asset discovered across your scans, aggregated into a single Cryptographic Bill of Materials. The charts at the top show the number of assets by type, classical risk, and quantum security level.

![](https://uploads.developerhub.io/prod/jdK6/drk53bahceeb8lyixhqp9cf6keipf66lmy8vt6ls6uqu1x68x718x0wdtgh47pcc.png)

For each asset you can see its type, quantum status, classical risk, overall verdict, quantum security level, security standard, and the number of jobs that reported it. Use the search field to find an asset by name, and the filter button to filter by type, quantum security level, or classical risk:

![](https://uploads.developerhub.io/prod/jdK6/f105lyg49f4qyhacea1ehr9fq8hs9p2j0c4d2d36kqx4gucemstt2x02cykd72dq.png)

Expand a row to see the classical security level, whether the asset is post-quantum cryptography, and the recommended replacements:

![](https://uploads.developerhub.io/prod/jdK6/zp7qpepa4nk4bxtp3jyywp4ew3ocev9kn6jwycgu8ngkum1muks4883s1goktrcc.png)

## Asset details

Click View asset details to open the asset page:

![](https://uploads.developerhub.io/prod/jdK6/qhht5npk0tmbujb1ysr8ytn25uwgflelgede0oul3r4dt1vwlio5j0chca0pl2r3.png)

The asset page shows:

- a warning banner, when the asset is weak against today's attacks;
- **Asset details:** the classical and quantum security levels, the NIST standard, the description, and the quantum rationale;
- **Recommended replacements:** the algorithms to use instead of this asset;
- **Files:** the files where the asset was found;
- **Jobs:** the scans that reported the asset;
- **Evidence:** the lines in the files that matched the asset.

The report of each scan has its own **Cryptography** tab. It shows the same view for that scan only, plus a **Worst files** card with the files that have the most assets that are not quantum safe:

![](https://uploads.developerhub.io/prod/jdK6/s4x0rwd04g48pavthlfgi888jsdi1e2z3fwc1w0tb3lxxgews31dotwgwxaduuok.png)

---

[All pages in this documentation](https://www.opswat.com/docs/supply-chain/llms.txt)
