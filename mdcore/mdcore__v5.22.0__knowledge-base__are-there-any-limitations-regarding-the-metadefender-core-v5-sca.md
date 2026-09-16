<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/are-there-any-limitations-regarding-the-metadefender-core-v5-sca -->

# Are there any limitations to the MetaDefender Core scan engines?

This article applies to all MetaDefender Core V4 and V5 releases deployed on Windows and Linux systems.

Yes.

Certain custom engines have limitations in terms of OS compatibility, maximum file size allowed for scanning, and supported file types.

The latest list of limitations is outlined below.

**File Size and OS Limitation**

| *Engine Name* | *File Size Limitation* | *OS Limitations* |
| --- | --- | --- |
| Antiy | 900 MB |  |
| Emsisoft | 4 GB |  |
| QuickHeal | 2 GB |  |
| RocketCyber Linux |  | Does not function on Redhat and CentOS versions earlier than 8.x. |
| Aurora |  | Does not function on Redhat and CentOS versions earlier than 8.x. |
| Nano AV |  | Does not function on Amazon Linux 2023 |
| SentinelOne | 4 GB |  |
| ClamAV | 5 MB (DeepScan disabled) Max scan size (DeepScan enabled) |  |

**Minimum System Resource Requirements**

| *Engine Name* | ***Minimum System Resource Requirements***  __ | *OS* |
| --- | --- | --- |
| ClamAV | 2GB + memory | Windows and Linux |
| IKARUS | 1GB shared memory in docker | Linux |

Warning:

ClamAV do not work on Redhat 8,9 if FIPS is enabled

Please Note:

For IKARUS, `--shm-size=1gb` should be added when starting the docker.

If you're using K8s, the section below should be specified in the yaml file

Please Note:

AhnLab’s engine is built several times a day. The main daily build is done at 6 PM Korea Standard Time (KST) the day before its version date. Because of this, the DB update may sometimes show the next day’s date — this is normal and follows the vendor’s process

YamlCopyspec:
volumes:
- name: dshm
emptyDir:
medium: Memory
containers:
- volumeMounts:
- mountPath: /dev/shm
name: dshm

**Supported File type for AI engines** **engines can be founded** [**here**](/docs/mdcore/v5.22.0/metascan-engines/supported-file-type)

**Additional Installed Services**

| *Engine Name* | *Installed Applications* |
| --- | --- |
| NETGATE | Spy Emergency (an icon will display on desktop) |

| *Engine Name* | Scan result |
| --- | --- |
| Bitdefender | Password-protected file's result will be returned "Not Scanned" for this engine. |

Please Note:

This list is accurate for the latest packages of custom engines.

Support:

If you need help navigating MetaDefender scan engine limitations, please follow these instructions on [How to Create Support Package With Bundle Tools?](/docs/mdcore/v5.22.0/troubleshooting/how-to-create-support-package-), before [creating a support case or chatting with our support engineer](https://my.opswat.com/portal/support).
