<!-- source: https://www.opswat.com/docs/filescan/troubleshooting/llm-configuration -->

# LLM Configuration

View as Markdown Ask ChatGPT about this page Ask Claude about this page

Most problems with dynamic scanning come from the connection between Aether and the LLM Harness Server, the model name, or the scan budget. Before changing any settings, run the two checks in Verifying the configuration from the Aether host. The access log of the inference server or gateway also shows whether requests from Aether arrive and how the server answers them.

| Symptom | Likely cause | What to check |
| --- | --- | --- |
| Connection refused or timeout | The LLM Harness Server is not reachable at that host and port | The inference server is running; the port is correct; firewall and network rules allow the traffic; the server is bound to a reachable address, not only to loopback |
| HTTP 401 or 403 | The API key is missing or incorrect | The key is sent as `Authorization: Bearer <key>` and matches the server's configuration |
| HTTP 404, "model not found" or similar | The served model name does not match the scanned file's name | The server serves the model under the scanned file's name without the extension, exactly as listed in `/v1/models`, with no typos and the correct casing |
| File or model name rejected | The name breaks the naming restrictions | The name follows the naming restrictions |
| HTTP 400 about chat templates or roles | The model does not support chat-style messages | Only chat-capable models are supported. Use an instruct or chat variant of the model, or confirm that the server exposes a chat endpoint. |
| Works locally on the LLM Harness Server but not from Aether | The endpoint is bound to loopback only, or a network policy blocks it | Bind the server to a reachable address, and open the port between Aether and the LLM Harness Server |
| `truncated: true` with many `probesTruncated` | The scan budget ran out before all probes ran | Increase the wall-clock budget, or make the target faster (GPU, model kept loaded) so that more probes fit in the budget |

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
