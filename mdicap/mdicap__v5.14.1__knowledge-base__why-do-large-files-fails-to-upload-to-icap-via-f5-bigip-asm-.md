<!-- source: https://www.opswat.com/docs/mdicap/v5.14.1/knowledge-base/why-do-large-files-fails-to-upload-to-icap-via-f5-bigip-asm- -->

# Why do large files fails to upload to ICAP via F5 BIGIP ASM?

This behavior applies to deployments where **F5 BIG-IP ASM** is used in front of a **MetaDefender ICAP server**.

When uploading files through **F5 BIG-IP ASM** to a **MetaDefender ICAP server**, files larger than **30 MB** fail to upload.

On the **F5 BIG-IP ASM**, the request is blocked with the violation:

> **“Request length exceeds defined buffer size”**

As a result, the file upload does not reach the MetaDefender ICAP server for scanning.

F5 BIG-IP ASM enforces limits on HTTP request buffering.

The parameter `long_request_buffer_size` controls the maximum size of HTTP requests that ASM can buffer and inspect.

- **Default value:** 10 MB
- **Maximum supported value:** 30 MB

If an HTTP request exceeds the configured buffer size, ASM triggers the violation:

> **Request length exceeds defined buffer size**

When this occurs, ASM blocks the request before it is forwarded to the backend server. Consequently, files larger than the configured limit (for example, **35 MB**) are **not sent to the MetaDefender ICAP server**.

To allow larger uploads, adjust the `long_request_buffer_size` setting in F5 BIG-IP ASM according to F5’s official guidance.

Refer to the F5 documentation:

- [myF5](https://my.f5.com/manage/s/article/K000153159)

Support:

If **Further Assistance** is required, please proceed to log a [**support case or chatting with our support engineer**](https://my.opswat.com/support).
