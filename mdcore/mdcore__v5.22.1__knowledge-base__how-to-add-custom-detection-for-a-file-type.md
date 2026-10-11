<!-- source: https://www.opswat.com/docs/mdcore/v5.22.1/knowledge-base/how-to-add-custom-detection-for-a-file-type -->

# How to add custom detection for a file type?

View as Markdown Ask ChatGPT about this page Ask Claude about this page Info:

The custom detection is only supported from File Type version 7.4 and later

Here are the step-by-step instructions to add a custom detection rule:

- **Identify a signature pattern of the file type** you wish to add custom detection for. Take a .des file as an example. It is a file encrypted using OpenSSL’s `enc` command with a salted password. Its well-known signature pattern is that the file content usually starts with `Salted__`. OpenSSL prepends this 8-byte header to indicate that the file was encrypted with a salted key derived from a password.

- Convert the signature pattern to a hexadecimal byte sequence
- You can use an online converter such as https

This hexadecimal byte sequence will be used to define the custom rule

- Open a Text editor and create a new text file
- Copy the following content into the new file

In this example, this rule is designed to detect files encrypted using **OpenSSL's** `enc` **command with a salted password**. Here's a detailed breakdown of what each important part of the rule does:

📘 `<Info>`**Section**

This section provides **metadata** about the custom rule:

`<description>openssl enc'd data with salted password</description>`

- Describes the rule’s intent: identify files encrypted with `openssl enc` using a password and salt.

<id>DES</id>

- Internal File Type ID of the rule. It’s labeled `DES`, but this ID is **arbitrary**—it could refer to the common usage of DES encryption in OpenSSL (e.g., `openssl enc -des -salt`), though other ciphers can also use the same salt header.

<mime>application/octet-stream</mime>

- Sets the **MIME type** for detected files. `application/octet-stream` is a generic binary file type.

`<group>OPENSSL_ENC</group>`

- Places this rule in the **OPENSSL_ENC** group, useful for organizing and classifying rules logically.

`<extension>des, dat<extension>`

- Assigns file **extensions** to this rule. Files with `.des` or `.dat` extensions that match the pattern will be recognized as matching this rule.

<Score>0.9</score>

- The score for this detection.

Important Notes:

The current use case is to turn an unknown (DATA) or not surely (non-DATA with score < 1.0) (detected by native rules of the engine) file type into a user-custom one with higher score.

There can be cases in which a file matches both a custom and a built-in rule. In order to prioritize the detection resulted from the custom rule, the custom rule should be defined with a high confidence score, e.g., 1.1.

#### [🧩<FrontBlock>](/docs/mdcore/v5.22.1/knowledge-base/how-to-add-custom-detection-for-a-file-type#frontblock)

This section defines the **byte pattern** that identifies the file format: <FrontBlock>

`<Pattern>`

Specifies a signature pattern.

`<Bytes>53616C7465645F5F</Bytes>`

- This is a **hexadecimal byte sequence** in the step #2

`<Pos>0</Pos>`

- Specifies the **offset** in the file where the signature must appear. In this case, the signature must be **at the beginning** of the file (byte position 0).

For details about the XML format with fields description, check [Rule definitions](/docs/mdcore/v5.22.1/utilities-engines/custom-detection#rule-definitions)

- Save the file with .xml extension
- Add the customer rule at MD Core UI > Inventory > Modules > Utilities > FileType engine > “Enable custom detection” > Input the path to the XML rule file

Check [Enable custom detection](/docs/mdcore/v5.22.1/utilities-engines/custom-detection#enable-custom-detection) to see how to enable custom detection

- Disable/Enable the FileType engine for the change to take effect.

- Scan the file with MD Core, you will see something like this in the File Type Verification section

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/portal/support).
