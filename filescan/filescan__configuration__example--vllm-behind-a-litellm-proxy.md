<!-- source: https://www.opswat.com/docs/filescan/configuration/example--vllm-behind-a-litellm-proxy -->

# Example Deployment

View as Markdown Ask ChatGPT about this page Ask Claude about this page

This is a minimal end-to-end setup on the LLM Inference Server. vLLM serves the model locally, and a LiteLLM proxy in front of it provides the Bearer-key authentication and the model alias that Aether expects. The example assumes that the file scanned by Aether is named `llama-3.2-3b.safetensors`, so Aether requests the model as `llama-3.2-3b`.

**Step 1: Start vLLM.** On the host that holds the model (typically the GPU machine), bound to an address LiteLLM can reach. If vLLM and LiteLLM run on the same host, `--host 127.0.0.1` is enough; if they run on separate hosts, bind vLLM to a reachable interface and allow the port from the LiteLLM host:

vllm serve meta-llama/Llama-3.2-3B-Instruct \
--host 127.0.0.1 --port 8000

**Step 2: Create the LiteLLM configuration file** (`litellm-config.yaml`). The `model_name` alias is the name that Aether requests, so it must equal the scanned file's name without the extension, with the exact same casing:

model_list:
- model_name: llama-3.2-3b # = scanned file name without extension (case-sensitive)
litellm_params:
model: hosted_vllm/meta-llama/Llama-3.2-3B-Instruct
api_base: http://127.0.0.1:8000/v1 # the local vLLM instance
api_key: "none" # vLLM itself has no authentication here
general_settings:
master_key: <bearer-key> # the Bearer key entered in Aether

**Step 3: Start LiteLLM**, bound to an address that Aether can reach:

litellm --config litellm-config.yaml --host 0.0.0.0 --port 4000

**Step 4: Configure Aether** with the base URL `http://<harness-host>:4000` and the master key as the API key. Aether sends `"model": "llama-3.2-3b"`, and LiteLLM authenticates the request and routes it to vLLM.

### Notes

- The name after the `hosted_vllm/` prefix must match the name that vLLM itself reports at its own `/v1/models`endpoint. By default, this is the model path or Hugging Face ID that vLLM was started with.
- LiteLLM does not reload its configuration automatically. Restart the proxy after editing the YAML file. vLLM can keep running, so the model stays loaded.
- Verify the setup with, the two checks in Verifying the configuration, using port 4000 and the Bearer key.

See the "Technical Datasheet" for a complete list of features: <https://docs.opswat.com/filescan/datasheet/technical-datasheet>
