<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/encrypted-traffic-visibility -->

# Encrypted Traffic Visibility

Most network traffic is now encrypted with Transport Layer Security (TLS). A sensor does not need the decryption keys to find threats in this traffic. The sensor inspects the parts of each connection that stay in cleartext. It also measures the shape and the behavior of the flow. This page explains how MetaDefender NDR gives visibility into encrypted traffic.

A sensor is passive. It reads a copy of the traffic from a mirror port or a network tap. The sensor does not sit inline. It does not break or slow the connection.

## [What the sensor sees without decryption keys](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#what-the-sensor-sees-without-decryption-keys)

A TLS or a QUIC connection starts with a handshake. The handshake is not encrypted. The sensor reads the handshake and extracts strong signals. The sensor also reads the packet sizes, the packet times, and the connection metadata. These signals stay visible even when the payload uses encryption.

The sensor extracts these data points from encrypted traffic:

- The TLS handshake parameters and the extensions.
- The server certificate and the full certificate chain.
- The Server Name Indication (SNI) value in the handshake.
- The negotiated protocol from Application-Layer Protocol Negotiation (ALPN).
- The source address, the destination address, and the port numbers.
- The packet count, the byte count, and the packet time for each direction.

## [TLS and QUIC fingerprints](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#tls-and-quic-fingerprints)

The sensor makes a fingerprint of each TLS handshake. A fingerprint is a hash of the handshake fields. The sensor supports the JA3 fingerprint for the client and the JA3S fingerprint for the server. The sensor also supports the newer JA4 fingerprint family. The JA4 family covers TLS and QUIC.

A fingerprint identifies the client software or the server software. This helps you find malware and command-and-control (C2) tools. A rare fingerprint or a known-bad fingerprint is a strong threat signal. The sensor keeps this ability even when the payload stays encrypted.

The sensor also fingerprints QUIC traffic. QUIC carries most HTTP/3 sessions. The sensor extracts the JA4 fingerprint and the ALPN value from the QUIC handshake.

## [Certificate analysis](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#certificate-analysis)

The server certificate is visible in most TLS handshakes. The sensor inspects the certificate for risk signals. The sensor checks these certificate properties:

- The validity period and the expiry date.
- The subject name and the issuer name.
- The certificate chain length.
- A self-signed certificate or an unusual issuer.
- A mismatch between the certificate and the SNI value.

A short validity period or a self-signed certificate is a common malware pattern. The sensor raises a detection when it finds these anomalies.

## [Statistical and flow analysis](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#statistical-and-flow-analysis)

The sensor measures the shape of each flow. This analysis works on the encrypted payload because it uses only the metadata. The sensor computes these statistics:

- The ratio of bytes out to bytes in. This is the Producer-Consumer Ratio (PCR).
- The inter-packet time and the packet size distribution.
- The connection duration and the session count.

A high PCR value can show data exfiltration. A long-duration connection with steady small packets can show a C2 beacon. The sensor detects these patterns from the flow statistics alone.

## [Protocol and handshake anomaly detection](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#protocol-and-handshake-anomaly-detection)

The sensor knows the correct structure of each protocol. It compares every handshake to this structure. The sensor reports an anomaly for these conditions:

- A malformed packet or an invalid handshake.
- An unusual handshake time.
- An ALPN value that does not match the port or the service.
- A TLS version or a cipher that your policy does not allow.

## [Machine learning on encrypted metadata](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#machine-learning-on-encrypted-metadata)

The sensor sends the encrypted-traffic metadata to the anomaly detection engine. The engine uses Random Cut Forests and other machine-learning models. The models learn the normal pattern of your network. The models use features such as the TLS handshake time, the DNS query entropy, and the netflow statistics. The engine raises an alert when a flow is far from the normal pattern.

## [Threat intelligence match](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#threat-intelligence-match)

The sensor matches the visible connection data against threat intelligence feeds. This match does not need the payload. The sensor checks these values in real time:

- The destination Internet Protocol (IP) address.
- The Autonomous System Number (ASN) and the country.
- The SNI hostname and the certificate fields.
- Known C2 infrastructure and Open-Source Intelligence (OSINT) indicators.

## [Optional decryption with break-and-inspect devices](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#optional-decryption-with-break-and-inspect-devices)

Some networks decrypt TLS at a break-and-inspect device, for example an A10 device or an F5 device. This device sends a copy of the decrypted traffic to a mirror port. A sensor accepts this decrypted traffic through the mirror.

Break-and-inspect is optional. MetaDefender NDR gives strong encrypted-traffic analytics without it. Use it only when your policy requires full payload inspection.

With decrypted traffic, the sensor performs full analysis. This includes deep protocol decode, file extraction, and signature detection on the cleartext payload.

## [Summary](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#summary)

MetaDefender NDR does not depend on decryption to protect encrypted traffic. The sensor uses fingerprints, certificate analysis, flow statistics, protocol anomalies, machine learning, and threat intelligence. Together these methods find threats in TLS and QUIC traffic. A break-and-inspect device adds full payload inspection when you need it.

## [See also](/docs/mdndr/deployment-guide/encrypted-traffic-visibility#see-also)

- Analysis methods performed by sensors
- Protocols supported for inspection and analysis
- ML anomaly detections
