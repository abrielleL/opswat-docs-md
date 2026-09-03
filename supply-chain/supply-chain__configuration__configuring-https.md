<!-- source: https://www.opswat.com/docs/supply-chain/configuration/configuring-https -->

# Configuring HTTPS

MetaDefender Software Supply-Chain can be configured to support **HTTPS** communication when accessing the Web UI and REST API.

### [Enable HTTPS on Unix-based deployments](https://www.opswat.com/docs/mdss/configuration/enabling-https#enable-https-on-unix-based-deployments)

For enabling HTTPS communication please follow these steps:

1. Obtain the **certificate** and the **private key** as two separate files (for example:  crt.pem & key.pem )
2. Rename the **private key** file in the form of <name>.key such that the extension of the file is .key
3. Place your certificates in ***/etc/mdssc/webclient/***
4. Run the ***enable_https***  utility by executing the following command:

```bash
sudo mdssc -u enable_https
```

5. Verify that **HTTPS** is configured correctly by navigating with your browser.

### [Disable HTTPS on Unix-based deployments](https://www.opswat.com/docs/mdss/configuration/enabling-https#disable-https-on-unix-based-deployments)

For disabling HTTPS communication, run the following command:

```bash
sudo mdssc -u disable_https
```

## Custom CA certificates

Custom certificates can be loaded in each **MDSSC** container by placing them in the appropriate configuration directory depending on the host OS. If the directory does not exist, an empty one is created at startup. Any number of certificates can be placed in the directory and they will be loaded into **MDSSC**.

### Configuring custom certificates on Linux

1. Certificates are loaded from the following path:

```bash
/etc/mdssc/ca_certificates/
```

2. After you add them to the specified folder above, restart **MDSSC** with the following command:

```bash
sudo mdssc -c restart
```

> **Warning**
>
> - Certificates should be in **.crt** **format**
> - The full SSL certificate chain should be loaded in MDSSC, especially if the certificate wasn't issued by a trusted CA
> - Root CAs and intermediate CAs can be loaded using the same procedure

### [Certificate validation for MetaDefender ](https://www.opswat.com/docs/mdss/configuration/custom-configuration#certificate-validation-for-metadefender-core-connection)Software Supply Chain

This environment variable controls certificate validation for **MetaDefender Software Supply Chain** integration during HTTP(S) requests. It is useful when **MetaDefender Software Supply Chain** needs to accept a partially valid certificate chain or a self-signed certificate.

You will need to edit **/etc/mdssc/customer.env** file and add the following environment variable with one of the values explained below:

```bash
MD_CORE_CERTIFICATE_VALIDATION=VALUE
```

#### Possible values

- **Default** → A MetaDefender Core server with invalid certificate can't be integrated
- **IgnoreChainErrors** → A MetaDefender Core server with certificate chain errors can be integrated
- **IgnoreAllErrors** → A MetaDefender Core server with invalid certificate can be integrated
