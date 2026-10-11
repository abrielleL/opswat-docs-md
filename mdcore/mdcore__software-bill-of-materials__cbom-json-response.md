<!-- source: https://www.opswat.com/docs/mdcore/software-bill-of-materials/cbom-json-response -->

# CBOM JSON response

View as Markdown Ask ChatGPT about this page Ask Claude about this page
## [JSON structure](/docs/mdcore/software-bill-of-materials/cbom-json-response#json-structure)

Inside a component, fields that have no value are **omitted entirely**; they are never returned as `null`, `""` or `[]`. Treat an absent key as "not known", not as "empty". The top-level `components` array is always present and is `[]` when no cryptographic assets were found.

JsonCopy"cbom_info": {
"final_verdict": { //scan-level summary; advisory only
"verdict": "<string>",
//"Verification Failed" | "No Cryptography Found" | "Unsafe Cryptography Found" | "Cryptography Found"
"verdict_explanation": ["<string>"], //one entry, equal to "verdict"
"blocked": false, //always false: CBOM never blocks a file
"severity": "INFO", //always "INFO"
"total_asset_count": <int>, //number of entries in "components"
"asset_counts": { //assets per type; all keys always present, zeros included
"algorithm": <int>,
"certificate": <int>,
"protocol": <int>,
"related_crypto_material": <int>,
"library": <int>
},
"risk_summary": {
"overall": { "safe": <int>, "unsafe": <int>, "unknown": <int> },
//safe + unsafe + unknown = total_asset_count
"classical": { "counts": { "acceptable": <int>, "deprecated": <int>, "disallowed": <int>, "unknown": <int> } },
"quantum": { "counts": { "quantum-safe": <int>, "quantum-weakened": <int>, "quantum-vulnerable": <int>, "unknown": <int> } }
}
},
"components": [
{
"uid": "<string>", //unique id of the asset: crypto/<type>/<name>@<hash>
"bom_ref": "<string>", //same value as "uid"
"name": "<string>",
"type": "cryptographic-asset",
"asset_type": "<string>", //same value as crypto_properties.asset_type
"crypto_properties": {
"asset_type": "<string>",
//"algorithm" | "certificate" | "protocol" | "related_crypto_material" | "library"
"description": "<string>",
"<asset_type>_properties": { }, //see "Type-specific properties"; not present for libraries
"risk": {
"overall": "<string>", //"safe" | "unsafe" | "unknown"
"classical": {
"level": "<string>", //"acceptable" | "deprecated" | "disallowed" | "unknown"
"strength": "<string>",
"safe": <boolean>
},
"quantum": {
"level": "<string>", //"quantum-safe" | "quantum-weakened" | "quantum-vulnerable" | "unknown"
"is_pqc": <boolean>,
"safe": <boolean>,
"rationale": "<string>",
"recommended_replacement": [ //present only when a replacement is recommended
{ "algorithm": "<string>", "nist_standard": "<string>" }
]
}
},
"evidences": [ //where the asset was found
{ "line": <int>, "match": "<string>" }
]
}
}
]
}
## [Type-specific properties](/docs/mdcore/software-bill-of-materials/cbom-json-response#type-specific-properties)

Each component carries one `*_properties` object inside `crypto_properties`, selected by `asset_type`:

| `asset_type` | Object | Fields |
| --- | --- | --- |
| `algorithm` | `algorithm_properties` | `algorithm_family`, `parameter_set_identifier`, `category`, `key_lengths[]`, `classical_security_level`, `nist_quantum_security_level`, `output_size`, `reference_primitive`, `performance`, `usage.recommended` |
| `certificate` | `certificate_properties` | `subject_name`, `issuer_name`, `certificate_format`, `description`, `not_valid_before`, `not_valid_after`, `public_key_length`, `signature_algorithm_ref`, `public_key_algorithm_ref`, `signature_algorithm_details`, `public_key_algorithm_details` |
| `protocol` | `protocol_properties` | `type`, `version`, `cipher_suites[]`, `usage.recommended` |
| `related_crypto_material` | `related_crypto_material_properties` | `type`, `algorithm_ref`, `key_lengths[]`, `min_key_length` |
| `library` | *(none)* | Library details are at the `crypto_properties` level: `vendor`, `library_type`, `library_supports[]`, `notes[]`, `detection_kind` |

For related crypto material, `algorithm_ref` holds the name of the algorithm the key or secret belongs to (for example `Ed25519`).

For certificates, `signature_algorithm_details` and `public_key_algorithm_details` are full algorithm objects, each with its own `risk` block. A certificate takes the weaker of its two algorithms' risk on each axis, so these objects explain why it was graded as it was. `public_key_algorithm_details.detected_key_length` is the key length measured from the certificate itself.

For libraries, `detection_kind` tells how the library was found: `declared-dependency` (named in a package manifest) or `link-flag` (only linked in a build script, so no version or package identity is available).

## [Field notes](/docs/mdcore/software-bill-of-materials/cbom-json-response#field-notes)

### [Risk](/docs/mdcore/software-bill-of-materials/cbom-json-response#risk)

- `overall_safe` is what the UI shows as **Overall Risk**: `safe`, `unsafe` or `unknown`. An asset is `unknown` when there is not enough information to grade it on one of the two axes (classical, quantum).
- When a level is `unknown`, the matching `safe` value is `false`. Read it as "not confirmed safe", not as "found unsafe".
- `quantum.is_pqc` names a mechanism and is distinct from the `quantum-safe` level: AES-256 is quantum-safe without being a post-quantum algorithm.
- `quantum.recommended_replacement` is an **array**, because there can be more than one successor. RSA, for example, needs ML-KEM (FIPS 203) for key establishment *and* ML-DSA (FIPS 204) for signatures; `applies_to` says which use each entry covers. If you need a single answer, read the first element.

### [Evidence](/docs/mdcore/software-bill-of-materials/cbom-json-response#evidence)

`evidences[].line` is the line where the asset was found and `match` is the matching text.

Certificates extracted from binary files are byte-offset findings, not line-based ones. Their entries carry `line: 0` by design, and the location is given in the `match` string:

- `pe_attribute_certificate_table@0x<offset>`: a certificate from the Windows PE attribute certificate table.
- `pe_embedded_pem@0x<offset>`: a PEM block embedded in the file.

### [Verdict](/docs/mdcore/software-bill-of-materials/cbom-json-response#verdict)

`verdict` is evaluated in this order:

1. `No Cryptography Found`: `total_asset_count` is 0.

2. `Unsafe Cryptography Found`: `risk_summary.overall.unsafe` is greater than 0.

3. `Cryptography Found`: all other cases, including when every asset is `safe` or `unknown`.

> **Note:** `No Cryptography Found` is returned both when an analyzed file yields no cryptographic assets and when the file type is not covered by CBOM analysis. The verdict does not distinguish between these two cases.

## [Examples](/docs/mdcore/software-bill-of-materials/cbom-json-response#examples)

### [A private key file](/docs/mdcore/software-bill-of-materials/cbom-json-response#a-private-key-file)

JsonCopy"cbom_info": {
"final_verdict": {
"verdict": "Unsafe Cryptography Found",
"verdict_explanation": ["Unsafe Cryptography Found"],
"blocked": false,
"severity": "INFO",
"total_asset_count": 1,
"asset_counts": { "algorithm": 0, "certificate": 0, "protocol": 0, "related_crypto_material": 1, "library": 0 },
"risk_summary": {
"overall": { "safe": 0, "unsafe": 1, "unknown": 0 },
"classical": { "counts": { "acceptable": 1, "deprecated": 0, "disallowed": 0, "unknown": 0 } },
"quantum": { "counts": { "quantum-safe": 0, "quantum-weakened": 0, "quantum-vulnerable": 1, "unknown": 0 } }
}
},
"components": [
{
"uid": "crypto/key/key_ed25519_private.key@sha256:<hash>",
"bom_ref": "crypto/key/key_ed25519_private.key@sha256:<hash>",
"name": "key_ed25519_private.key",
"type": "cryptographic-asset",
"asset_type": "related_crypto_material",
"crypto_properties": {
"asset_type": "related_crypto_material",
"description": "Modern signature scheme over Curve25519.",
"related_crypto_material_properties": {
"type": "private-key",
"algorithm_ref": "Ed25519",
"key_lengths": [256]
},
"risk": {
"overall": "unsafe",
"classical": { "level": "acceptable", "strength": "strong", "safe": true },
"quantum": {
"level": "quantum-vulnerable",
"is_pqc": false,
"safe": false,
"rationale": "Edwards-curve discrete logarithm broken by Shor's algorithm.",
"recommended_replacement": [ { "algorithm": "ML-DSA", "nist_standard": "FIPS 204" } ]
}
},
"evidences": [ { "line": 1, "match": "Parsed from file: key_ed25519_private.key" } ]
}
}
]
}

### [A library declared in a Maven `pom.xml` (one component shown)](/docs/mdcore/software-bill-of-materials/cbom-json-response#a-library-declared-in-a-maven-pomxml-one-component-shown)

JsonCopy{
"uid": "crypto/library/Tink@<hash>",
"bom_ref": "crypto/library/Tink@<hash>",
"name": "Tink",
"type": "cryptographic-asset",
"asset_type": "library",
"crypto_properties": {
"asset_type": "library",
"description": "Misuse-resistant cryptography library with opinionated key management.",
"vendor": "Google",
"library_type": "crypto-toolkit",
"detection_kind": "declared-dependency",
"library_supports": ["AES-GCM", "AES-SIV", "ChaCha20-Poly1305", "ECDSA", "Ed25519", "HKDF"],
"notes": ["Exposes intents (AEAD, signing) rather than raw primitives, which removes most parameter-choice mistakes"],
"risk": {
"overall": "unknown",
"classical": { "level": "acceptable", "strength": "strong", "safe": true },
"quantum": {
"level": "unknown",
"is_pqc": false,
"safe": false,
"rationale": "Insufficient information to determine post-quantum risk."
}
},
"evidences": [ { "line": 14, "match": "<groupId>com.google.crypto.tink</groupId>" } ]
}
}
