<!-- source: https://www.opswat.com/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera -->

# Is MetaDefender OT Access affected by the Brotli decoder vulnerability (CVE-2026-111497)?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [Answer](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#answer)

No. MetaDefender OT Access is not affected by CVE-2026-111497. The affected library is present in some container images, but no product component passes attacker-controlled data to the Brotli decoder. No workaround or configuration change is required.

## [About the vulnerability](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#about-the-vulnerability)

CVE-2026-111497 is a memory-safety vulnerability in the Brotli decoder (`BrotliDecoderDecompress*`). A crafted compressed stream can cause an out-of-bounds write, which can lead to a crash or code execution.

To exploit it, an attacker needs both:

- A vulnerable Brotli decoder in the target process.
- A way to deliver attacker-controlled data to that decoder.

## [Why MetaDefender OT Access is not affected](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#why-metadefender-ot-access-is-not-affected)

Several MetaDefender OT Access container images include the Debian package `libbrotli1` 1.0.9-2, which is in the affected range. None of the following components passes attacker-controlled data to the decoder:

| Component | Why it cannot be reached |
| --- | --- |
| HTTP traffic inspection | Does not contain or link a Brotli decoder. Traffic sent with `Content-Encoding: br` is not decompressed. |
| Outbound HTTP clients (libcurl) | Response decompression is not enabled, so libcurl does not request or decode Brotli-encoded responses. |
| Management console and scripts (Python) | The Python `brotli` and `brotlicffi` packages are not installed, so HTTP libraries do not request or decode Brotli. |
| Browser access (remote desktop rendering) | FreeType uses Brotli only to open WOFF2 fonts. Browser access uses the fonts installed in the image; a remote session cannot supply fonts. |
| Reverse proxy (nginx) | Built without Brotli support. |

No product component bundles its own copy of the Brotli decoder.

## [Affected versions](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#affected-versions)

None. All supported versions of MetaDefender OT Access are unaffected.

## [Action required](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#action-required)

None for MetaDefender OT Access.

A vulnerability scan of MetaDefender OT Access can still report `libbrotli1` 1.0.9-2 as vulnerable, because scanners check only the package version. A future release will include the patched package `libbrotli1` 1.0.9-2+deb12u1.

## [References](/docs/metadefender-ot-access/knowledge-base/is-metadefender-ot-access-affected-by-the-brotli-decoder-vulnera#references)

- CVE-2026-111497
- Debian security tracker for brotli: https://security-tracker.debian.org/tracker/source-package/brotli

Last reviewed: October 2026
