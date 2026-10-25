<!-- source: https://www.opswat.com/docs/mdicap/v5.15.0/operating/risks-with-range-request -->

# Risks with range request

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Hypertext Transfer Protocol (HTTP) clients often encounter interrupted data transfers as a result of canceled requests or dropped connections. When a client has stored a partial representation, it is desirable to request the remainder of that representation in a subsequent request rather than transfer the entire representation. Likewise, devices with limited local storage might benefit from being able to request only a subset of a larger representation, such as a single page of a very large document, or the dimensions of an embedded image. [[RFC 7233](https://tools.ietf.org/html/rfc7233)]

Both clients and servers support requesting or sending only parts of the original content based on the request of the client. The fact that a content was sent in fragments is hidden form the end user in most of the cases, it may happen automated by the client and the server to optimize performance.

In most of the cases MetaDefender ICAP Server requires, however, the whole object, so that it can detect malicious contents.

When the content is delivered utilizing range requests, then there is no way for the ICAP Server to have the object as a whole. As a consequence in these cases ICAP Server may not be able to detect existing malicious code in the whole object, as it is assembled at the client side only.

Info

The reason why ICAP needs the whole object is, that certain malware detection methods are based on signatures (similar to hashing), that may be completely different, when only part of the malicious code is available.

As the ICAP protocol is request / response based (similarly to REST) it is also not possible for the ICAP Server to wait for all fragments of the whole object and assemble it for scanning on the ICAP Server side.

Warning

As a consequence, when range requests are in use, chopped malicious contents may remain undetected by the ICAP Server, and get allowed.

When the client reassembles the original object from the fragments, the resulted contents may be malicious.
