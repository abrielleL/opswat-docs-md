<!-- source: https://www.opswat.com/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json -->

# Base64-encoded data in JSON

### [JSON](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#json)

JSON data can contain base64-encoded data within certain attributes. For example:

JsonCopy{
"user": {
"id": "12345",
"name": "John Doe",
"profilePicture": "data:image/png;base64,iVBORw0KGgoAAAAN...",
"photos": [
{
"id": "photo1",
"description": "A scenic view",
"image": "asset:oc6neh5prnji..."
},
{
"id": "photo2",
"description": "A portrait",
"image": "asset:2y8nslo98gur..."
}
]
},
"metadata": {
"timestamp": "2024-12-24T12:00:00Z",
"source": "Generated Example"
},
"data": {
"image1": "R0lGODlhAQABAIAAAISwxwAAACwAAAAAAQABAAACAkQBADs=",
"image2": "iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAgMAAABinRfyAA...",
"images": [
"/9j/4AAQSkZJRgABAQEAeAB4AAD/4QAiRXhpZgAATU0AKg...",
"iVBORw0KGgoAAAANSUhEUgAAABAA..."
]
}
}

Deep CDR can be configured to perform an in-depth inspection of such data by:

- Decoding base64-encoded content.
- Recursively sanitizing the extracted data.
- Re-encoding the sanitized data in base64.
- Reinserting the processed data back into the JSON structure.

#### [Configuration](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#configuration)

This feature can be enabled at **Workflow Management> Workflows > [Workflow name] > Deep CDR > Advanced configuration > File type handling > Others > JSON > Process Base64 encoded data**.

- **Data following "data" URL scheme**: Base64 encoded data that start with "data" URL scheme, e.g., data:image/png;base64,iVBORw0K.
- **Data at certain JSON path**: Regular expressions of JSON path to fields to be processed, e.g., user..*Picture$.
- **Action on data when sanitization not applied:** Choose what action should be applied to data when sanitization is not supported or fails

#### [Regular expression examples](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#regular-expression-examples)

Below are some examples on regular expressions and corresponding JSON nodes from an example JSON that match with the expressions.

JsonCopy{
"data": {
"image1": "R0lGODlhAQABAIAAAISwxwAAACwAAAAAAQABAAACAkQBADs=",
"image2": "iVBORw0KGgoAAAANSUhEUgAAABAAAAAQAgMAAABinRfyAA...",
"images": [
"/9j/4AAQSkZJRgABAQEAeAB4AAD/4QAiRXhpZgAATU0AKg...",
"iVBORw0KGgoAAAANSUhEUgAAABAA..."
]
}
}

| Expression | JSON node at path that matches |
| --- | --- |
| data.image1 | data.image1 |
| data.images.0 | data.images[0] |
| data.images..* | data.images[0], data.images[1] |
| data.image.* | data.image1, data.image2, data.images[0], data.images[1] |

Node: item index in a JSON array starts from 0.

### [XML](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#xml)

#### [Configuration](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#configuration)

This feature can be enabled at **Workflow Management> Workflows > [Workflow name] > Deep CDR > Advanced configuration > File type handling > Others > XML > Process Base64 encoded data**.

XmlCopy<root>
<file1>SGVsbG8gV29ybGQhIFRoaXMgaXMgYSBzaW1wbGUgdGV4dCBmaWxlLg==</file1>
<file2 name="invalid.jpg" content="/9j/4AAQSkZJRgABAQEAeAB4AAD/4QAiRXhpZgAATU0AKgAAAAgAAQESAAMAAAABAAEAAAAAAAD/"/>
<files name="icon.png" content1="iVBORw0KGgoAAAANSUhEUgAAAAEAAAABCAYAAAAfFcSJAAAADUlEQVR42mNk+M9QDwADhgGAWjR9awAAAABJRU5ErkJggg==">
<content2>R0lGODlhAQABAIAAAISwxwAAACwAAAAAAQABAAACAkQBADs=</content2>
</files>
</root>
#### [Regular expression examples](/docs/mdcore/v5.21.0/deep-cdr/base64-encoded-data-in-json#regular-expression-examples)

| Expression | **XML node/attribute at path that matches** |
| --- | --- |
| root.file1 | root.file1 |
| root.file2.content | root.file2.content |
| root.files.content.* | root.files.content1, root.files.content2 |
| root.files..* | root.files.name, root.files.content1, root.files.content2 |
| root.file.* | root.file1, root.file2.name, root.file2.content, root.files.name, root.files.content1, root.files.content2 |
