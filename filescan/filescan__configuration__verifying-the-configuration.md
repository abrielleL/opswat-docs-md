<!-- source: https://www.opswat.com/docs/filescan/configuration/verifying-the-configuration -->

# Verifying the Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Before running Aether against the LLM Inference Server, confirm that the model is available under the name that Aether will use. Run these checks from a host with the same network access as Aether, ideally the Aether host itself.

### [List the served models](/docs/filescan/configuration/verifying-the-configuration#list-the-served-models)

Confirm that the endpoint is reachable and that the expected model name is in the list:

curl http://<harness-host>:<port>/v1/models \
-H "Authorization: Bearer <api-key-if-required>"

The response lists the model IDs that the server accepts. The scanned file's name without the extension must appear here exactly, with the same casing.

### [Send a test request](/docs/filescan/configuration/verifying-the-configuration#send-a-test-request)

Confirm that the model responds to a chat completion request that uses the same model name. This also confirms that the model is chat-capable, because the request uses the same `/v1/chat/completions` endpoint as Aether:

curl http://<harness-host>:<port>/v1/chat/completions \
-H "Authorization: Bearer <api-key-if-required>" \
-H "Content-Type: application/json" \
-d '{
"model": "<file-name-without-extension>",
"messages": [{"role": "user", "content": "Reply with the single word: ready"}]
}'

A well-formed response with model output confirms that the base URL, the served model name, chat capability and authentication are all correct. If this request succeeds, Aether can reach the model with the same settings.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
