<!-- source: https://www.opswat.com/docs/mdndr/deployment-guide/analysis-methods-performed-by-sensors -->

# Analysis Methods Performed by Sensors

The sensor performs multiple layers of analysis in real time:

- **Signature-based detection**: Traditional Suricata rules (ET Pro + custom) with fast_pattern and rich metadata.
- **Machine learning-based anomaly detection**: Random Cut Forests, Isolation Forests (and evaluated alternatives) on protocol features and netflow statistics. Protocol features include DNS entropy/volume, HTTP UA anomalies, and TLS handshake time.
- **Behavioral anomaly detection**: RisingWave materialized views for behavioral-based detection.
- **Statistical anomaly detection**: Netflow analysis for exfiltration (bytes out/in ratio) and long-duration connections.
- **Protocol anomaly detection**: Malformed packets, unusual handshake time, ALPN mismatches.
- **High-fidelity threat intelligence**: Real-time match against C2, TI, and OSINT feeds (IPs, domains, URLs, hashes).

**Encrypted traffic analysis** (performed even without decryption keys):

- Statistical analysis of netflow (packet/byte ratios, inter-packet time).
- TLS certificate analysis (validity period, subject/issuer anomalies, chain length).
- IP analysis and match to threat intelligence (suspicious ASNs, countries, known C2 infrastructure).
- JA3 and JA4 fingerprint of client and server TLS parameters.
