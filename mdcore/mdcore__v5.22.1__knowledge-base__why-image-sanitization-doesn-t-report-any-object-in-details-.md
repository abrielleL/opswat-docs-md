<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/why-image-sanitization-doesn-t-report-any-object-in-details- -->

# Why image sanitization doesn't report any object in details?

View as Markdown Ask ChatGPT about this page Ask Claude about this page

The most common way attackers hide malicious code in images is through a technique called steganography, where they secretly embed code within the pixels. Later, they use a special method to extract and run the hidden code. Since it's almost impossible to spot this hidden code without knowing exactly how and where it's concealed, Deep CDR doesn't try to detect it. Instead, Deep CDR focuses on disrupting the image's pixel data so the attacker's method for retrieving the hidden code no longer works. In this process, Deep CDR doesn't remove or sanitize any object in the image.

For more image attack vectors and how Deep CDR can help, please refer to this blog post: [How Emerging Image-Based Malware Attacks Threaten Enterprise Defenses](https://www.opswat.com/blog/how-emerging-image-based-malware-attacks-threaten-enterprise-defenses)

Support:

If **Further Assistance** is required, please proceed to [create a support case or chat with our support engineer](https://my.opswat.com/portal/support).
