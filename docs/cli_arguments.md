# CLI Arguments and Flags

llamafile accepts two layers of command-line options:

1. Wrapper flags added by llamafile itself, such as `--server`, `--chat`, `--cli`, and `--gpu`.
2. The bundled `llama.cpp` flags that are passed through to chat, CLI, and server mode.

For the exact help text on your current build, run:

```sh
llamafile --server --help
llamafile --chat --help
llamafile --cli --help
```

`llamafile --server --help` prints the broadest list. `--chat` and `--cli` accept the shared `llama.cpp` flags too, plus a small number of mode-specific wrapper flags.

## Commonly Used Flags

| Flag | What it does |
| --- | --- |
| `-t, --threads N` | Number of CPU threads to use during generation. |
| `-tb, --threads-batch N` | Number of CPU threads to use during prompt and batch processing. |
| `-c, --ctx-size N` | Context window size. `0` means to use the model default. |
| `-b, --batch-size N` | Logical maximum batch size. |
| `-ub, --ubatch-size N` | Physical maximum batch size. |
| `--mlock` | Keep the model in RAM instead of letting the OS swap or compress it. |
| `--repeat-penalty N` | Penalize repeating tokens during sampling. `1.0` disables the penalty. |
| `-ngl, --gpu-layers, --n-gpu-layers N` | Number of layers to offload to GPU. |
| `--host HOST` | Server bind address. |
| `--port PORT` | Server listen port. |

## Wrapper and Mode Flags

- Mode selection: `--server`, `--chat`, `--cli`
- Common wrapper flags: `-m FILE`, `-p TEXT`, `--gpu MODE`, `-ngl N`, `--verbose`, `--version`, `--help`
- Chat-only wrapper flags: `--nologo`, `--ascii`
- CLI-only wrapper flags: `--nothink`

## Shared Flags Accepted by Chat, CLI, and Server

### General, CPU, Context, and Batching

- General help and shell integration: `-h`, `--help`, `--usage`, `--version`, `-cl`, `--cache-list`, `--completion-bash`, `--verbose-prompt`
- CPU scheduling and affinity: `-t`, `--threads`, `-tb`, `--threads-batch`, `-C`, `--cpu-mask`, `-Cr`, `--cpu-range`, `--cpu-strict`, `--prio`, `--poll`, `-Cb`, `--cpu-mask-batch`, `-Crb`, `--cpu-range-batch`, `--cpu-strict-batch`, `--prio-batch`, `--poll-batch`
- Context and batching: `-c`, `--ctx-size`, `-n`, `--predict`, `--n-predict`, `-b`, `--batch-size`, `-ub`, `--ubatch-size`, `--keep`, `--swa-full`, `-fa`, `--flash-attn`
- Prompt input: `-p`, `--prompt`, `-f`, `--file`, `-bf`, `--binary-file`, `-e`, `--escape`, `--no-escape`
- RoPE and YaRN: `--rope-scaling`, `--rope-scale`, `--rope-freq-base`, `--rope-freq-scale`, `--yarn-orig-ctx`, `--yarn-ext-factor`, `--yarn-attn-factor`, `--yarn-beta-slow`, `--yarn-beta-fast`

### Memory, KV Cache, and Offload

- KV cache and host memory: `-kvo`, `--kv-offload`, `-nkvo`, `--no-kv-offload`, `--repack`, `-nr`, `--no-repack`, `--no-host`
- Cache storage and defragmentation: `-ctk`, `--cache-type-k`, `-ctv`, `--cache-type-v`, `-dt`, `--defrag-thold`
- Memory mapping and residency: `--mlock`, `--mmap`, `--no-mmap`, `--numa`, `--check-tensors`, `--op-offload`, `--no-op-offload`
- Draft-model cache types: `-ctkd`, `--cache-type-k-draft`, `-ctvd`, `--cache-type-v-draft`

### Devices, GPU, Tensors, and Adapters

- Devices and tensor placement: `-dev`, `--device`, `--list-devices`, `-ot`, `--override-tensor`
- CPU MoE controls: `-cmoe`, `--cpu-moe`, `-ncmoe`, `--n-cpu-moe`
- GPU offload controls: `-ngl`, `--gpu-layers`, `--n-gpu-layers`, `-sm`, `--split-mode`, `-ts`, `--tensor-split`, `-mg`, `--main-gpu`
- Automatic fitting: `-fit`, `--fit`, `-fitt`, `--fit-target`, `-fitc`, `--fit-ctx`
- Adapters and metadata overrides: `--lora`, `--lora-scaled`, `--control-vector`, `--control-vector-scaled`, `--control-vector-layer-range`, `--override-kv`

### Model Selection, Downloads, and Logging

- Model path and downloads: `-m`, `--model`, `-mu`, `--model-url`, `-dr`, `--docker-repo`
- Hugging Face and related model selectors: `-hf`, `-hfr`, `--hf-repo`, `-hfd`, `-hfrd`, `--hf-repo-draft`, `-hff`, `--hf-file`, `-hfv`, `-hfrv`, `--hf-repo-v`, `-hffv`, `--hf-file-v`, `-hft`, `--hf-token`
- Logging and diagnostics: `--log-disable`, `--log-file`, `--log-colors`, `-v`, `--verbose`, `--log-verbose`, `--offline`, `-lv`, `--verbosity`, `--log-verbosity`, `--log-prefix`, `--log-timestamps`, `--perf`, `--no-perf`

## Sampling Flags

- Sampling order and randomness: `--samplers`, `-s`, `--seed`, `--sampler-seq`, `--sampling-seq`, `--ignore-eos`
- Core sampling controls: `--temp`, `--top-k`, `--top-p`, `--min-p`, `--top-nsigma`, `--xtc-probability`, `--xtc-threshold`, `--typical`
- Repetition controls: `--repeat-last-n`, `--repeat-penalty`, `--presence-penalty`, `--frequency-penalty`
- DRY and dynamic temperature: `--dry-multiplier`, `--dry-base`, `--dry-allowed-length`, `--dry-penalty-last-n`, `--dry-sequence-breaker`, `--dynatemp-range`, `--dynatemp-exp`
- Mirostat and constrained output: `--mirostat`, `--mirostat-lr`, `--mirostat-ent`, `-l`, `--logit-bias`, `--grammar`, `--grammar-file`, `-j`, `--json-schema`, `-jf`, `--json-schema-file`

## CLI and Chat-Specific Flags

- Output and interaction: `--display-prompt`, `--no-display-prompt`, `-co`, `--color`, `--show-timings`, `--no-show-timings`, `-cnv`, `--conversation`, `-no-cnv`, `--no-conversation`, `-st`, `--single-turn`, `-mli`, `--multiline-input`, `--simple-io`
- System prompt and stopping: `-sys`, `--system-prompt`, `-sysf`, `--system-prompt-file`, `-r`, `--reverse-prompt`, `-sp`, `--special`
- Context and cache management: `--ctx-checkpoints`, `--swa-checkpoints`, `-cram`, `--cache-ram`, `--context-shift`, `--no-context-shift`, `--warmup`, `--no-warmup`
- Parallel decode and multimodal input: `-np`, `--parallel`, `-mm`, `--mmproj`, `-mmu`, `--mmproj-url`, `--mmproj-auto`, `--no-mmproj`, `--no-mmproj-auto`, `--mmproj-offload`, `--no-mmproj-offload`, `--image`, `--audio`, `--image-min-tokens`, `--image-max-tokens`
- Draft and speculative decoding: `-otd`, `--override-tensor-draft`, `-cmoed`, `--cpu-moe-draft`, `-ncmoed`, `--n-cpu-moe-draft`, `--draft`, `--draft-n`, `--draft-max`, `--draft-min`, `--draft-n-min`, `--draft-p-min`, `-cd`, `--ctx-size-draft`, `-devd`, `--device-draft`, `-ngld`, `--gpu-layers-draft`, `--n-gpu-layers-draft`, `-md`, `--model-draft`, `--spec-replace`
- Chat templates and reasoning controls: `--chat-template-kwargs`, `--jinja`, `--no-jinja`, `--reasoning-format`, `--reasoning-budget`, `--chat-template`, `--chat-template-file`
- Built-in defaults: `--gpt-oss-20b-default`, `--gpt-oss-120b-default`, `--vision-gemma-4b-default`, `--vision-gemma-12b-default`

`-np, --parallel` in CLI and chat mode controls the number of parallel sequences to decode.

## Server-Only Flags

- Server runtime and batching: `-kvu`, `--kv-unified`, `--spm-infill`, `--pooling`, `-np`, `--parallel`, `-cb`, `--cont-batching`, `-nocb`, `--no-cont-batching`, `--threads-http`, `--cache-reuse`
- Network and API configuration: `-a`, `--alias`, `--host`, `--port`, `--path`, `--api-prefix`, `--api-key`, `--api-key-file`, `-to`, `--timeout`
- Web UI and monitoring: `--webui-config`, `--webui-config-file`, `--webui`, `--no-webui`, `--metrics`, `--props`, `--slots`, `--no-slots`, `--slot-save-path`
- Router and media: `--media-path`, `--models-dir`, `--models-preset`, `--models-max`, `--models-autoload`, `--no-models-autoload`
- Embeddings, reranking, and TLS: `--embedding`, `--embeddings`, `--rerank`, `--reranking`, `--ssl-key-file`, `--ssl-cert-file`
- Chat templating and slot behavior: `--chat-template-kwargs`, `--jinja`, `--no-jinja`, `--reasoning-format`, `--reasoning-budget`, `--chat-template`, `--chat-template-file`, `--prefill-assistant`, `--no-prefill-assistant`, `-sps`, `--slot-prompt-similarity`, `--lora-init-without-apply`, `--sleep-idle-seconds`
- Draft, speculative decoding, and TTS: `-td`, `--threads-draft`, `-tbd`, `--threads-batch-draft`, `--draft`, `--draft-n`, `--draft-max`, `--draft-min`, `--draft-n-min`, `--draft-p-min`, `-cd`, `--ctx-size-draft`, `-devd`, `--device-draft`, `-ngld`, `--gpu-layers-draft`, `--n-gpu-layers-draft`, `-md`, `--model-draft`, `--spec-replace`, `-mv`, `--model-vocoder`, `--tts-use-guide-tokens`
- Built-in server defaults: `--embd-gemma-default`, `--fim-qwen-1.5b-default`, `--fim-qwen-3b-default`, `--fim-qwen-7b-default`, `--fim-qwen-7b-spec`, `--fim-qwen-14b-spec`, `--fim-qwen-30b-default`, `--gpt-oss-20b-default`, `--gpt-oss-120b-default`, `--vision-gemma-4b-default`, `--vision-gemma-12b-default`

`-np, --parallel` in server mode controls the number of server slots rather than the number of parallel decode sequences.

## Notes

- The lists above reflect the bundled `llama.cpp` help surfaced by this repo.
- If you are unsure whether a flag is shared, CLI-only, or server-only, check `llamafile --server --help`, `llamafile --chat --help`, and `llamafile --cli --help`.
