<!-- source: https://www.opswat.com/docs/filescan/configuration/requirements -->

# Requirements

View as Markdown Ask ChatGPT about this page Ask Claude about this page
### 1. OpenAI-compatible API and chat model

The endpoint must accept standard OpenAI-style chat completion requests. In practice, it must respond to:

POST http://<harness-host>:<port>/v1/chat/completions

with a JSON body that contains a `model` field and a `messages` array, and return a standard OpenAI-format response. Most modern inference servers support this by default.

The target model itself must support chat. Aether sends all of its probe requests to `/v1/chat/completions`, so only chat-capable (chat or instruct) models can be scanned dynamically. A base model without a chat template usually fails these requests with an error about chat templates or message roles. If the model is available only as a base variant, serve its chat or instruct variant instead.

Servers such as Ollama that also offer their own native API are supported only through their OpenAI-compatible `/v1`endpoints, not through the native API.

### 2. Network reachability

The host address (IP address or host name) and port of the LLM Inference Server must be reachable from the environment where Aether runs. Make sure that:

- The inference server is bound to an address that Aether can reach, not only to `127.0.0.1` (loopback).
- Every firewall, security group or network policy between Aether and the LLM Inference Server allows traffic to the chosen port.

### 3. Model name

Aether infers the model name from the file name of the scanned model file by removing the file extension, and sends that name in the `model` field of every request. For example, when the scanned file is `llama-3.2-3b.gguf`, Aether sends requests with `"model": "llama-3.2-3b"`.

The LLM Inference Server must therefore serve the target model under exactly that name. The match is exact and case-sensitive, so configure the served model name to match the scanned file's name (without the extension) character for character. The method depends on how the model is served:

- On vLLM, use `--served-model-name <file-name-without-extension>`.
- On Ollama, create or alias the model under a tag equal to that name (for example, with `ollama cp`).
- Behind a gateway or proxy such as LiteLLM, set the `model_name` alias to that name. The LiteLLM configuration file is case-sensitive, so the alias must match the casing of the file name exactly.

Alternatively, rename the file before uploading it, so that its name is the served model ID plus the extension that matches its actual format.

#### Naming restrictions

The file name, and therefore the model name, must meet these restrictions:

- Only readable ASCII characters are allowed.
- These special characters are not allowed: `\` `/` `:` `*` `?` `"` `<` `>` `|`
- Multiple consecutive underscores are not allowed (for example, `invalid__name` is not accepted).
- The name must not be an empty string.

Choose a file name that follows these rules, or rename the file, and serve the model under the same name. To confirm that the server exposes the name as expected, get the list of served model IDs from the endpoint (see Verifying the configuration).

#### Models split into several files

Some models are distributed as several files, for example sharded SafeTensors (`model-00001-of-00004.safetensors`) or split GGUF parts. In this case the parts do not need to be merged into one file, and not every part needs to be uploaded to Aether. It is enough to upload one file that:

- has the same file type (format and extension) as the model served by the LLM Inference Server, and
- has the correct name: the served model ID plus the file extension, as described above.

If necessary, rename that part so that its name matches the served model ID exactly. Aether only derives the model name from the uploaded file. The model that actually answers the probe requests is the one served by the LLM Inference Server.

### 4. Authentication

Aether supports one authentication method: a Bearer key sent in the Authorization header (`Authorization: Bearer <key>`). This is the same scheme that a LiteLLM proxy uses for its master key. No other authentication method is supported. In particular, custom API-key headers, JWT or OAuth tokens, mutual TLS (client certificates) and provider-specific signed requests cannot be used to reach the LLM Inference Server.

This means the LLM Inference Server must be one of the following:

- **Unauthenticated.** This is common for internal-only deployments, for example a vLLM or Ollama server on a trusted network. No key is configured in Aether.
- **Protected by a Bearer key.** The most common way is to put a LiteLLM proxy in front of the model server. The proxy checks the Bearer key, and the same key is entered in Aether.

If the model server uses an authentication method other than a Bearer key, put a LiteLLM proxy (or an equivalent gateway that accepts a Bearer token) in front of it, and point Aether at the proxy.

For any endpoint that requires a key, use HTTPS instead of plain HTTP, so that the key is not sent over the network in clear text.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
