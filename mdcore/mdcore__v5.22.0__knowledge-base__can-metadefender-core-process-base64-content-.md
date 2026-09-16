<!-- source: https://www.opswat.com/docs/mdcore/v5.22.0/knowledge-base/can-metadefender-core-process-base64-content- -->

# Can MetaDefender Core process Base64 Content?

Yes, MetaDefender Core is capable of decoding and processing Base64 Encoded files.

It is possible to send a Base64 Encoded string using the API Call features.

For example, we took the following PDF File and encoded it:

Resulting in a string:

JVBERi0xLjcNCiW1tbW1DQoxIDAgb2JqDQo8PC9UeXBlL0NhdGFsb2cvUGFnZXMgMiAwIFIvTGFuZyhlbikgL1N0cnVjdFRyZWVSb290IDI4IDAgUi9NYXJrSW5mbzw8L01hcmtlZCB0cnVlPj4vTWV0YWRhdGEgNTQgMCBSL1ZpZXdlclByZWZlcmVuY2VzIDU1IDAgUj4…………………

Using Postman, we prepared a POST message to <protocol>://<md_core_address>:8008/file URI, enabling Content-Encoding header, with the base64 as the given value.

And pasted the Base64 Encoded string in an empty file which we uploaded as binary:

After which we have sent the message and obtained a result:

Additionally, we can send the string as a Raw Body base64 text string:

Checking the MetaDefender Core’s History, we have found that the sent file has been correctly decoded, for both methods:

We can check the HASH against the original file and see they are all the same:
