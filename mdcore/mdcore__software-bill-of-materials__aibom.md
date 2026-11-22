<!-- source: https://www.opswat.com/docs/mdcore/software-bill-of-materials/aibom -->

# AI Bill of Materials (AIBOM)

View as Markdown Ask ChatGPT about this page Ask Claude about this page Connect your AI tool
## [What an AIBOM is](/docs/mdcore/software-bill-of-materials/aibom#what-an-aibom-is)

An AI Bill of Materials (AIBOM) is an inventory of the AI and machine-learning model files in a scan: what each model file is, what its own bytes declare about it, and which public repositories are known to publish exactly those bytes.

An SBOM answers *which third-party packages are in this artifact*. An AIBOM answers the provenance question an SBOM cannot: *this model file arrived in our pipeline — what is it, where does it come from, and under what license?*

## [How it works](/docs/mdcore/software-bill-of-materials/aibom#how-it-works)

AIBOM reads two things: the bytes of the scanned file, and an **offline model database** that ships with the engine. It identifies a model by the SHA-256 of its bytes and looks that digest up in the database.

- **No network access.** The lookup runs entirely against the local database, so an air-gapped deployment gets the same result as a connected one.
- **No risk rating.** AIBOM reports what it read and what it looked up. It makes no claim about whether a model is safe to load.
- **Works without a match.** When a file matches no known repository, AIBOM still reports what the file's own header declares, such as format, parameter count and architecture.

## [Supported model formats](/docs/mdcore/software-bill-of-materials/aibom#supported-model-formats)

AIBOM scans a file only when its extension **and** the file type MetaDefender Core detects from its content both match a row below. A file that matches no row reports **No AI Components Found**.

| **Format** | **Files** |
| --- | --- |
| **GGUF** | `.gguf`, `.gguf-split-a`, `.gguf.part1of<N>` (first part only), `.lora`, `.mmproj`, `.oasr` |
| **SafeTensors** | `.safetensors`, `.sft`, `.st`, `.q4nx` |
| **ONNX** | `.onnx`, `.axmodel`, `.pt` (ONNX content only) |
| **Keras** | `.keras` |
| **PyTorch** (TorchScript) | `.jit`, `.ptl`, `.torchscript` |
| **PyTorch 2 export** | `.pt2` |
| **NVIDIA NeMo** | `.nemo` |
| **llamafile** | .`llamafile` |
| **CycloneDX AIBOM** | `.json` (CycloneDX 1.5 or later) |

AIBOM also reads CycloneDX JSON reports with `specVersion` 1.5 or later (the version that introduced the `machine-learning-model` component type). Each `machine-learning-model` component, with its `modelCard`, becomes an AIBOM component. The AIBOM database is not needed for this path. The Block Base Models and Block Model Types lists, and the AI license list, still apply. A report with no `machine-learning-model` component returns **No AI Components Found**. Reports older than 1.5 are not read by AIBOM.

## [What gets reported](/docs/mdcore/software-bill-of-materials/aibom#what-gets-reported)

Each scan reports one **component group** for the scanned file and a list of **components**, one per public repository that publishes that file byte for byte.

- **The component group is the file.** It carries the file's SHA-256, the name it was submitted under, and what its header declares. These facts come from the bytes on disk, so they are always current.
- **Components are repositories, not files.** A model file is often published by several repositories: mirrors, re-uploads and forks. Each becomes its own component, with that repository's name, revision, license and model details. Several components mean several candidate identities for **one** file.
- **Disagreements stay visible.** Repositories that publish identical bytes often declare different licenses or tasks. AIBOM reports all of them rather than picking one, so a license conflict is visible to your policy instead of being resolved arbitrarily.

A file that matches no known repository is reported as a single component of type `machine-learning-model`, named as it was submitted, with the uid `ai/model/<file name>@sha256:<digest>`. A component matched to a repository has the uid `pkg:huggingface/<owner>/<model>@<commit>`, without `@<commit>` when no commit still holds the file.

## [License classification](/docs/mdcore/software-bill-of-materials/aibom#license-classification)

Each license a repository declares is checked against the **Block Model Licenses** list in the AIBOM Module. This list is separate from the SBOM license policy, so blocking a license for packages does not block it for models. Block Model Licenses is off by default. Its list comes pre-filled with the non-commercial and no-derivatives Creative Commons licenses (CC-BY-NC-2.0/3.0/4.0, CC-BY-NC-ND-3.0/4.0, CC-BY-NC-SA-2.0/3.0/4.0, CC-BY-ND-4.0) and Proprietary, and these take effect as soon as you turn the option on. The option is available only when license risk detection is enabled in the SBOM database.

| Result | **Meaning** |
| --- | --- |
| Allowed | The repository declared a license that is not selected in Block Model Licenses, or the option is off. |
| Blocked | The repository declared a license selected in Block Model Licenses, and the option is on |
| Unknown | The repository declared no license, or the file matched no repository |

> **Note:** Only a recognized license can be blocked. A license string that AIBOM does not recognize, such as `openrail`, is always reported as allowed, whatever the policy says.

## [AIBOM verdict](/docs/mdcore/software-bill-of-materials/aibom#aibom-verdict)

AIBOM gives each scan one of five verdicts:

- **AI Components Found**: model files were found and none is blocked.
- **License Risk Found**: at least one component declares a license selected in **Block Model Licenses**.
- **Base Model Risk Found**: at least one component matches a **Block Base Models** pattern.
- **Model Type Risk Found**: at least one component's model type matches a **Block Model Types** pattern.
- **No AI Components Found**: the file holds no AI or machine-learning content.

When more than one risk applies, the verdict is the first in the order License Risk Found, Base Model Risk Found, Model Type Risk Found, and `verdict_explanation` lists each one that applies, in that order. Each of the three risk verdicts blocks the file. AIBOM never raises the severity of a scan: its severity is always `INFO`.

**Blocking by base model and model type**

Two options in the AIBOM Module block models by name. Both are off by default and start with an empty list.

- **Block Base Models** blocks a model when its name, its base model, or any model it derives from matches one of the patterns. Names read `owner/model`, as on Hugging Face. A model the database does not know is named after the uploaded file.
- **Block Model Types** blocks a model when its model type matches one of the patterns. The model type is the `model_type` in the model's `config.json`, such as `bert`, `llama` or `qwen3`.

Write one regular expression per row. Matching ignores case and finds the pattern anywhere in the value unless you anchor it with `^` or `$`. Look-around and backreferences are not supported. Examples: `^deepseek-ai/` blocks every deepseek-ai model and every model derived from one; `^qwen` blocks `qwen2`, `qwen3` and `qwen3_moe`.

A blocked component carries `model_card.blocked_by.base_model` or `model_card.blocked_by.model_type`, each holding `matched_pattern` (the first pattern that matched) and `matched_value` (the name or type it matched).

For the full result structure, see [AIBOM JSON response](aibom-json-response).

## [Enabling AIBOM](/docs/mdcore/software-bill-of-materials/aibom#enabling-aibom)

AIBOM requires MetaDefender Core 5.23.0 or later and is **enabled by default**. Its settings are in the **AIBOM Module** section of Workflow > [workflow name] > SBOM. **Enable AI Bill of Materials (AIBOM)** turns the module on or off. Its three blocking options (**Block Model Licenses**, **Block Base Models**, **Block Model Types**) are off by default. Scanning model files requires the AIBOM offline database, which is delivered with the SBOM database package; CycloneDX documents are read without it. On Core versions earlier than 5.23.0 the AIBOM section is not shown and AIBOM does not run.
