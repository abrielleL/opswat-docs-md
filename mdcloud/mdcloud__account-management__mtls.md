<!-- source: https://www.opswat.com/docs/mdcloud/account-management/mtls -->

# mTLS

As many organizations are required by their security team and/or governing body to leverage mTLS to provide an additional layer of security, OPSWAT's MetaDefender Cloud does offer that option to its customers.

Info

Please note that mTLS is only available for our customers on the enterprise tier of MetaDefender Cloud. For more information about the enterprise tier and all the additional benefits/features that come with it, please visit our [licensing page](https://metadefender.opswat.com/licensing).

What is mTLS?

Mutual TLS, or mTLS for short, is a method for mutual authentication. mTLS ensures that parties on both ends of a network connection are who they say they are by verifying that they both have the correct private key. The information within their respective TLS certificates provides additional verification to ensure a high level of security. Many organizations are being required to use mTLS to encrypt communication.

mTLS is a modified version of TLS (Transport Layer Security). It uses the same protocols and technologies, it's just a two-way verification instead of one

## [How mTLS works](/docs/mdcloud/account-management/mtls#how-mtls-works)

Here are the high level steps for establishing an mTLS connection

1. The client send a request to the server.
2. The server sends an acknowledgement of that request back to the client.
3. The server sends the TLS certificate and requests the client to send its certificate to verify that the client is who they say they are.
4. The client sends the certificate (along with additional information) to the server, verifying the client's identity.
5. Now the communication between the client and server endpoints is established and encrypted.

## [I Want to Use mTLS, What Steps Do I Need to Take?](/docs/mdcloud/account-management/mtls#i-want-to-use-mtls-what-steps-do-i-need-to-take)

#### [From your side:](/docs/mdcloud/account-management/mtls#from-your-side)

The first thing that OPSWAT will need from your side is a TLS certificate. OPSWAT will load that certificate on one of our servers to help authenticate the requests coming from your organization.

You can get your TLS certificate from one of three places:

- a publicly trusted certificate authority (CA) such as GoDaddy
- you can generate a self-signed cert from your internal CA *(note that if you choose this option, you will need to provide OPSWAT with the entire chain of trust for your self-signed cert)*
- an open certificate authority *(we do not recommend this one as these certs expire and have to be updated every 3 months)*

The other thing that we will need from your side is a slight alteration to your requests to MetaDefender Cloud. The only change that needs to be made is including your certificate and private key in your requests. This will help us distinguish your organization's traffic from that of our other customers. The private key that you will need to pass in the request will be provided to you by the authority that issued your TLS certificate.

#### [From the OPSWAT side:](/docs/mdcloud/account-management/mtls#from-the-opswat-side)

On our side our cloud operations team will stand up the necessary servers to accommodate your mTLS requests as well as set up your organization with a custom endpoint. This endpoint will only be accessible by sending requests with the correct certificate and private key. All other requests will be rejected as they will not fulfill the necessary conditions for mTLS.

#### [Example Request](/docs/mdcloud/account-management/mtls#example-request)

Here is an example request for submitting a file for scanning using mTLS. Please note the custom endpoint, key, and cert that need to be added to your request to leverage mTLS.

BashCopycurl --location --request POST 'https://<custom endpoint>.api.metadefender.com/v4/file'
--key <key path> \
--cert <cert path> \
--header 'apikey: <api key>' \
--header 'Content-Type: application/octet-stream' \
--header "filename: {filename}" \
--header "archivepwd: {archivepwd}" \
--header "filepassword: {filepassword}" \
--header "samplesharing: {samplesharing}" \
--header "privateprocessing: {privateprocessing}" \
--header "downloadfrom: {downloadfrom}" \
--header "rule: {rule}" \
--header "sandbox: {sandbox}" \
--header "sandbox_timeout: {sandbox_timeout}" \
--header "sandbox_browser: {sandbox_browser}" \
--header "callbackurl: {callbackurl}" \
--header "rescan_count: {rescan_count}" \
--header "rescan_interval: {rescan_interval}" \
--data '"@/path/to/data.file"'
## [mTLS FAQs](/docs/mdcloud/account-management/mtls#mtls-faqs)

**I am not an enterprise customer, can I still use mTLS**

Unfortunately mTLS is only available for customers on our enterprise tier. If you would like to upgrade to our enterprise tier to take advantage of mTLS and other benefits/features please reach out to [sales-inquiry@opswat.com](mailto:sales-inquiry@opswat.com).

**What should I name the certificate?**

You can name the certificate whatever you want. As long as we have that certificate and that it is included in the header of your requests you will be good to use mTLS.

**Where do I get a private key?**

The private key will be provided to you by the certificate authority that issued your TLS certificate.
