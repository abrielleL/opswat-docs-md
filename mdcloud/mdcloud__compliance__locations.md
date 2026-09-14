<!-- source: https://www.opswat.com/docs/mdcloud/compliance/locations -->

# Locations

MetaDefender Cloud is a global cloud product designed to satisfy the needs of clients all around the world. The actual physical location of the servers hosting a cloud product is important, mainly because of the following aspects:

- Speed: a cloud service located closer to its users has faster response times
- Privacy: due to certain privacy requirements, organizations may require that their data does not leave the perimeter of the country or continent.

We value the experience and privacy of our users. Our service is provided by servers located in the following locations:

- North America (United States, West coast)
- Europe Central (Germany)
- Canada (Montreal)
- Australia (Sydney)
- Japan (Tokyo)
- India (Mumbai)
- Israel (Tel Aviv)

The existing locations have been chosen based on our users. Every time a user calls the service, the request will be directed to the location closest to the caller’s physical location. In case users want to force use one of the locations, please call:

- For North America: [https://api-prod-uswest2.metadefender.com](https://api-prod-uswest2.metadefender.com/)
- For Europe: [https://api-prod-eucentral1.metadefender.com](https://api-prod-eucentral1.metadefender.com/)
- For Canada: [https://api-prod-cacentral1.metadefender.com](https://api-prod-cacentral1.metadefender.com/)
- For Australia: [https://api-prod-apsoutheast2.metadefender.com](https://api-prod-apsoutheast2.metadefender.com/)
- For Japan: [https://api-prod-apnortheast1.metadefender.com](https://api-prod-apnortheast1.metadefender.com/)
- For India: [https://api-prod-apsouth1.metadefender.com](https://api-prod-apsouth1.metadefender.com/)
- For Israel: [https://api-prod-ilcentral1.metadefender.com](https://api-prod-ilcentral1.metadefender.com/)

The files uploaded do not leave the designated server location. For example, customer files uploaded to North American server will be stored and processed in North America.

All files are automatically encrypted when stored. Unless using private scanning, files will be stored in one of the above locations for an indefinite period of time.

If your organization has special needs which require a data center in a different location, please [contact](https://www.opswat.com/contact) sales to discuss the opportunity of adding a new location to our list.

### [Data Flow Diagram](/docs/mdcloud/compliance/locations#data-flow-diagram)

Below is a data flow example of how a file would be routed through the US and EU infrastructure (same would apply for all other regions).
