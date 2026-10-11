<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-metadefender-core---s-nginx-ssl-conf-changed-to-ssl-mdcore-c -->

# Why MetaDefender Core’s nginx ssl.conf changed to ssl.mdcore.conf?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

This article applies to all MetaDefender Core versions starting with 5.13.

Starting with version 1.24.0 of Nginx, the ssl directive has been deprecated and can no longer be used for configuring SSL. To address this, MetaDefender Core updated the naming convention of **ssl.conf to ssl.mdcore.conf**.

#### [Implications and limitations](/docs/mdcore/v5.22.1/knowledge-base/why-metadefender-core---s-nginx-ssl-conf-changed-to-ssl-mdcore-c#implications-and-limitations)

The implications of this are that the **ssl, ssl_certificate** and **ssl_certificate_key** directives will be placed in the **ssl.mdcore.conf**. The current limitation is that the file does not support the following directives: **ssl_client_certificate, ssl_verify_client, ssl_verify_depth**.

In this scenario, the configuration can be achieved as follows:

**ssl.conf.mdcore file:**

`ssl`

`ssl_certificate`

`ssl_certificate_key`

**ssl.conf file:**

`ssl_client_certificate`

`ssl_verify_client`

`ssl_verify_depth`

Info:

Starting with MetaDefender Core version 5.14.0, advanced configuration can be achieved directly via the User Interface, without the need of having an individual config file: [Enabling HTTPS](/docs/mdcore/v5.22.1/configuration/enabling-https)

This way the configurations are stored internally and not being exposed to an external file.

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
