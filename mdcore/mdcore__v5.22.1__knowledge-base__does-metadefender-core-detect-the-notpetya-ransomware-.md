<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware- -->

# Does MetaDefender Core v5 Detect the NotPetya Ransomware?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Check Your Version:

This article applies to all MetaDefender Core releases subsequent to V4.21.2, including all V5 releases, deployed on Windows or Linux systems.

The voracious NotPetya ransomware attacks were first detected in Ukraine in 2017 and quickly spread across Europe and the world, continuing on their devastating course for approximately two years.

Please Note:

OPSWAT was swift to incorporate defenses against this threat into the latest MetaDefender Core technology and, since the group responsible for the NotPetya attacks are still at large today, we (and our vendors) remain vigilant and dedicated to safeguarding organizations against NotPetya and similar threats.

At the heart of the solution, the base MetaDefender Core multi-scanning engine uses up to 33 anti-malware engines to scan files for threats. Our detection rate is dependent on the number of enabled engines, with a higher number of engines increasing malware detection rates overall.

Currently, most of the engines included in our MetaDefender Core base packages acknowledge the NotPetya ransomware threat. Below is a package breakdown with relevant information provided by each of the engine vendors.

Please Note:

1. Lower packages of MetaDefender Core are subsets of higher packages. So, higher packages include the same engines as lower packages - plus more.
2. For a comprehensive list of engines per package and OS, expand the **Metascan** tab on the following webpage: [MetaDefender Enterprise Licensing](https://www.opswat.com/products/metadefender/enterprise)
3. Some of our vendors may already be detecting the NotPetya threat but do not have any official post about it. These vendors are not listed below but will be included as more information becomes available.
4. Specific engine detection is based on the most up-to-date engine definitions. Some latency may occur due to update frequency, update methods, or network speeds.
## [**Windows**](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#windows)

### [***MetaDefender Core 8***](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#metadefender-core-8)

Avira:

[Petya strikes back - Avira Blog](https://www.avira.com/en/blog/petya-strikes-back)

ESET:

[“Petya” Ransomware: What we know now | | ESET](https://www.eset.com/us/about/newsroom/corporate-blog/petya-ransomware-what-we-know-now/)

Bitdefender:

[Massive GoldenEye Ransomware Campaign Slams worldwide users](https://www.bitdefender.com/en-us/blog/labs/massive-goldeneye-ransomware-campaign-slams-worldwide-users)

[MBR-Encrypting Ransomware Petya Gets Bitdefender Vaccine](https://www.bitdefender.com/en-us/blog/labs/low-level-petya-ransomware-gets-bitdefender-vaccine)

[Petya Ransomware Goes Low Level](https://www.bitdefender.com/en-us/blog/labs/petya-ransomware-goes-low-level)

Quick Heal:

[Petya ransomware is affecting users globally, here are things you can do](https://blogs.quickheal.com/petya-ransomware-affecting-users-globally-things-can/)

VirITeXplorer:

[Petya or notPetya ? questo è il dilemma.... nuovo ransomware o vecchia conoscenza...](https://www.tgsoft.it/news/news_archivio.asp?id=843)

### [***MetaDefender Core 12***](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#metadefender-core-12)

CYREN:

[Petya Ransomware Rises by Using Similar Exploit As WannaCry - Cyren](https://data443.com/petya-ransomware-spreading-fast-using-same-wannacry-exploit/)

### [***MetaDefender Core 16***](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#metadefender-core-16)

Emsisoft:

[Petya ransomware variant attacks computers worldwide](https://www.emsisoft.com/en/blog/27836/petya-petna-ransomware/)

Zillya!:

[Кибертака Украина: В антивирусной компании рассказали, кто может стоять за хакерской атакой Petya.A и чем это грозит — Украина](https://tsn.ua/ru/ukrayina/v-antivirusnoy-kompanii-rasskazali-kto-mozhet-stoyat-za-hakerskoy-atakoy-petya-a-i-chem-eto-grozit-885812.html)

VirusBlokAda:

[New Ransomworm Follows WannaCry Exploits](https://www.fortinet.com/blog/threat-research/new-ransomware-follows-wannacry-exploits)

### [MetaDefender Core 20](https://docs.opswat.com/mdcore/knowledge-base/does-metadefender-core-v4-detect-the-notpetya-ransomware-#metadefender-core-20)

McAfee:

[How to protect against Petya, Ransom-WannaCry, and other ransomware | McAfee Support](https://www.mcafee.com/support/s/article/000001792?language=en_US)

[How to Protect Against Petya Ransomware in a McAfee Environment | McAfee Blog](https://www.mcafee.com/blogs/other-blogs/mcafee-labs/protect-petya-ransomware-mcafee-environment/)

Sophos:

[Petya variants behind global ransomware outbreak – Sophos News](https://news.sophos.com/en-us/2017/06/27/petya-variants-behind-global-ransomware-outbreak/)

[Troj/Petya-AQ - Viruses and Spyware - Advanced Network Threat Protection | ATP from Targeted Malware Attacks and Persistent Threats | sophos.com - Threat Center](https://www.sophos.com/en-us/threat-center/threat-analyses/viruses-and-spyware/Troj~Petya-AQ)

## [**Linux**](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#linux)

### [***MetaDefender Core 5***](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#metadefender-core-5)

Bitdefender:

[Massive GoldenEye Ransomware Campaign Slams worldwide users](https://www.bitdefender.com/en-us/blog/labs/massive-goldeneye-ransomware-campaign-slams-worldwide-users)

[Petya Ransomware Goes Low Level](https://www.bitdefender.com/en-us/blog/labs/petya-ransomware-goes-low-level)

ESET: [“Petya” Ransomware: What we know now | | ESET](https://www.eset.com/us/about/newsroom/corporate-blog/petya-ransomware-what-we-know-now/)

### [***MetaDefender Core 10***](/docs/mdcore/v5.22.1/knowledge-base/does-metadefender-core-detect-the-notpetya-ransomware-#metadefender-core-10)

Avira:

[Petya strikes back - Avira Blog](https://www.avira.com/en/blog/petya-strikes-back)

CYREN:

[Petya Ransomware Rises by Using Similar Exploit As WannaCry - Cyren](https://data443.com/petya-ransomware-spreading-fast-using-same-wannacry-exploit/)

Quick Heal:

[Petya ransomware is affecting users globally, here are things you can do](https://blogs.quickheal.com/petya-ransomware-affecting-users-globally-things-can/)

---

Support:

For more information on virus-specific protections, or to report a suspected vulnerability or threat, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.1/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
