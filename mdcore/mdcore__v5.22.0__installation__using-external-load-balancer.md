<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/installation/using-external-load-balancer -->

# Using external Load Balancer

## [Application Load Balancing (Layer 7)](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#application-load-balancing-layer-7)

This page provides information about recommended ways to use sessions with a Layer 7 load-balancer.

Most load-balancers have the ability to provide cookies for pinning subsequent traffic from a client to the appropriate server. This method is called sticky session, session persistence or session affinity. Using cookies efficiently requires the client to know when a cookie should be sent, should not be sent or should be deleted.

### [Sticky session load balancing](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#sticky-session-load-balancing)

Each MetaDefender Core instance has its own databases and application sessions that cannot be seen by other instances. Therefore, in order to get the related data/response to our queries we should ask the appropriate MetaDefender Core v5 server. On the other hand, to keep the advantages of the used load balancing method, cookies should not be sent if it is not necessary.

#### [Single file scanning](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#single-file-scanning)

| Step | Stage | Task | Cookie usage |
| --- | --- | --- | --- |
|  | Sending file | Initiate processing a file on the client side. Send file through the load-balancer. (See [POST File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysispost)) | Cookie should not be sent |
|  | Sending file | Save the cookie and the data_id you got from the load-balancer | Save cookie |
|  | Getting result | Request result related to data_id saved in step 2. (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)) | Send cookie saved in step 2 |
|  | Getting result | If processing is in progress (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)), wait a little while and repeat step 3. | Send cookie saved in step 2 |

#### [Batch scanning](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#batch-scanning)

| Step | Stage | Task | Cookie usage |
| --- | --- | --- | --- |
|  | Open batch | Initiate processing file(s) in batch. Request a batch ID through the load-balancer. (See [POST Initiate Batch](/docs/mdcore/v5.22.0/metadefender-core#batchcreate)) | Cookie should not be sent |
|  | Open batch | Save the cookie and the batch_id you got from a Core server through the load-balancer. | Save cookie |
|  | Sending files | Send file through the load-balancer. (See [POST File Analysis (using batch header)](/docs/mdcore/v5.22.0/metadefender-core#fileanalysispost)) | Send cookie saved in step 2 |
|  | Sending files | Save the data_id you got from the load-balancer. |  |
|  | Sending files | Status/result of scanning of sent files can be queried: (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)) | Send cookie saved in step 2 |
|  | Sending files | Repeat step 3-4. with files wanted to be in the same batch. |  |
|  | Getting batch status | See [GET Batch Status](/docs/mdcore/v5.22.0/metadefender-core#batchstatus) | Send cookie saved in step 2 |
|  | Close batch | Tell the server that no more files will be sent to this batch. (See [POST Close Batch](/docs/mdcore/v5.22.0/metadefender-core#batchclose)). (This will only be successful if all the files sent to the batch have been processed already. Repeat this step until batch is closed.) | Send cookie saved in step 2 |
|  | Getting results | Request results related to batch ID saved in step 2. (See [GET Download Batch Signed Result](/docs/mdcore/v5.22.0/metadefender-core#batchsignedresult) | Send cookie saved in step 2 |

If it does not matter which upstream server responds, the queries should be sent without cookie.

Info

It is recommended not to send cookies when it's not necessary to allow load-balancer to use its own method to share the load between MetaDefender Core v5 servers.

### [Limitations, additional notes](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#limitations-additional-notes)

Using load-balancing between MetaDefender Core servers does not support:

- Global scan history
- Core server administration through load-balancer

#### [OPSWAT products that support HTTP load balanced MetaDefender Cores](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#opswat-products-that-support-http-load-balanced-metadefender-cores)

| Product name | Minimum version |
| --- | --- |
| MetaDefender Kiosk | 4.3.4 |
| MetaDefender Endpoint | Windows: 7.6.247.0 Mac: 10.4.243.0 |
| MetaDefender Email Gateway Security | 4.3.0 |
| MetaDefender ICAP Server | 4.3.0 |
| MetaDefender Managed File Transfer | 1.3.0 |
| MetaDefender Storage Security | 2.0.7 |

## [DNS Load Balancing](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#dns-load-balancing)

Using this method is logically similar to Layer 7 load-balancing.

### [Briefly how it works](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#briefly-how-it-works)

Client uses a domain name to send a query to a server. Client's DNS server has more "A" records for that name with different IPs. When a client resolves the server's domain name DNS server randomly chooses an IP for that name to send back. When a session is used on the application layer, client should know the IP address of the Core server that handles that specific session. In every other case, client should resolve the domain name with DNS query to let requests to be balanced between MetaDefender Core servers.

#### [Single file scanning](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#single-file-scanning)

| Step | Stage | Task | Addressing |
| --- | --- | --- | --- |
|  | Choose a Core server by using DNS load balancing | Resolve the Core servers' common domain name. | Use domain name |
|  | Choose a Core server by using DNS load balancing | Save the IP gotten from the DNS server. | Save the IP |
|  | Sending file | Initiate processing a file on the client side. (See [POST File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysispost)) | Use IP saved in step 2 |
|  | Sending file | Save the data_id got from the Core server |  |
|  | Getting result | Request result related to data_id saved in step 2. (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)) | Use IP saved in step 2 |
|  | Getting result | If processing is in progress (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)), wait a little while and repeat step 3. | Use IP saved in step 2 |

#### [Batch scanning](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#batch-scanning)

| Step | Stage | Task | Addressing |
| --- | --- | --- | --- |
|  | Choose a Core server by using DNS load balancing | Resolve the Core servers' common domain name. | Use domain name |
|  | Choose a Core server by using DNS load balancing | Save the IP gotten from the DNS server. | Save the IP |
|  | Open batch | Initiate processing file(s) in batch. Request a batch ID. (See [POST Initiate Batch](/docs/mdcore/v5.22.0/metadefender-core#batchcreate)) | Use IP saved in step 2 |
|  | Sending files | Send file to the specific Core server with the basch ID saved in step 3. (See [POST File Analysis (using batch header)](/docs/mdcore/v5.22.0/metadefender-core#fileanalysispost)) | Use IP saved in step 2 |
|  | Sending files | Save the data_id you got from the Core server. |  |
|  | Sending files | Status/result of scanning of sent files can be queried: (See [GET File Analysis](/docs/mdcore/v5.22.0/metadefender-core#fileanalysisget)) | Use IP saved in step 2 |
|  | Sending files | Repeat step 3-4. with files wanted to be in the same batch. |  |
|  | Getting batch status | See [GET Batch Status](/docs/mdcore/v5.22.0/metadefender-core#batchstatus) | Use IP saved in step 2 |
|  | Close batch | Tell the server that no more files will be sent to this batch. (See [POST Close Batch](/docs/mdcore/v5.22.0/metadefender-core#batchclose)). (This will only be successful if all the files sent to the batch have been processed already. Repeat this step until batch is closed.) | Use IP saved in step 2 |
|  | Getting results | Request results related to batch ID saved in step 2. (See [GET Download Batch Signed Result](/docs/mdcore/v5.22.0/metadefender-core#batchsignedresult)). | Use IP saved in step 2 |

### [Limitations, additional notes](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#limitations-additional-notes)

Using load-balancing between MetaDefender Core servers does not support:

- Global scan history
- Core server administration via DNS load-balancing

#### [OPSWAT products that support DNS load balanced MetaDefender Cores](/docs/mdcore/v5.22.0/installation/using-external-load-balancer#opswat-products-that-support-dns-load-balanced-metadefender-cores)

| Product name | Minimum version |
| --- | --- |
| MetaDefender Kiosk | does not support yet |
| MetaDefender Endpoint | does not support yet |
| MetaDefender Email Gateway Security | does not support yet |
| MetaDefender ICAP Server | does not support yet |
| MetaDefender Managed File Transfer | does not support yet |
