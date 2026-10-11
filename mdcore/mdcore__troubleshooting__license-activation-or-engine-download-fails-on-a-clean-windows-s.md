<!-- source: https://www.opswat.com/docs/mdcore/troubleshooting/license-activation-or-engine-download-fails-on-a-clean-windows-s -->

# License activation or engine download fails on a clean Windows Server environment

View as Markdown Ask ChatGPT about this page Ask Claude about this page

**Applies to:** MetaDefender Core installed on a clean Windows Server environment

### [Symptoms](/docs/mdcore/troubleshooting/license-activation-or-engine-download-fails-on-a-clean-windows-s#symptoms)

- MetaDefender Core installs and starts normally.
- The server has internet access. Browsers and other tools on the same server can reach the internet, and the MetaDefender Core update server is reachable.
- One of the following issues occurs:

  - Online activation fails with the error: `Could not connect to the activation server. Check your Internet connection or use offline activation method`
  - Activation succeeds, but the engines are never downloaded.

### [Confirm the cause](/docs/mdcore/troubleshooting/license-activation-or-engine-download-fails-on-a-clean-windows-s#confirm-the-cause)

The MetaDefender Core log contains the following errors:

[WARNING] (common.communication) SSL errors while downloading file, url='https://activation.dl.opswat.com/activation?...'
[WARNING] (common.communication) Certificate chain for the ssl error, ...
[WARNING] (common.communication) Certificate chain item, index='1', ... issuerCommonName='QList("Amazon Root CA 1")', ... subjectCommonName='QList("Amazon RSA 2048 M01")'
[WARNING] (common.communication) Certificate chain item, index='2', ... issuerCommonName='QList("Starfield Services Root Certificate Authority - G2")', ... subjectCommonName='QList("Amazon Root CA 1")'
[WARNING] (common.communication) SSL error, error='...'
[WARNING] (common.update) Activation error, see error code, error='5'
[ERROR ] (common.update) Error during activating the product, errorString='Could not connect to the activation server...'
### [Root Cause](/docs/mdcore/troubleshooting/license-activation-or-engine-download-fails-on-a-clean-windows-s#root-cause)

The activation server's certificate is issued by Amazon. It chains up to **Starfield Services Root Certificate Authority - G2**, a root certificate that Microsoft trusts.

Windows does not install all trusted root certificates up front. It downloads each one from Windows Update the first time a Windows program needs it. On a newly installed server, nothing has needed this root yet, so it is not in the certificate store.

MetaDefender Core does not trigger that download. It checks certificates against the roots already in the store, and it reads the store **when the service starts**. With the root missing, Core rejects the connection and reports it as a connection failure.

### [Solution](/docs/mdcore/troubleshooting/license-activation-or-engine-download-fails-on-a-clean-windows-s#solution)

In most cases, restarting the MetaDefender Core service resolves the issue, because the service reloads the certificate store when it starts.
