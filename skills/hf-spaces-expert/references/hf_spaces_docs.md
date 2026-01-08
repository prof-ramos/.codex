# Hugging Face Spaces docs map (local)

Use these local docs under /Users/gabrielramos/DoclingSpace/hub-docs-docs-hub for factual checks and citations.
Prefer searching with rg before opening full files.

## Core files and key facts

- spaces-overview.md
  - Default limits: 16GB RAM, 2 CPU cores, 50GB ephemeral disk (free tier).
  - Secrets/Variables: set in Settings; for non-Docker Spaces both are env vars.
  - Helper env vars: SPACE_ID, SPACE_HOST, CPU_CORES, MEMORY, etc.
  - Networking: ports 80/443/8080 only.

- spaces-config-reference.md
  - README.md YAML metadata: title, sdk, app_file, sdk_version, python_version, etc.
  - suggested_hardware / suggested_storage fields.
  - preload_from_hub for build-time downloads.

- spaces-dependencies.md
  - requirements.txt, pre-requirements.txt, packages.txt conventions.

- spaces-storage.md
  - Persistent storage mounted at /data; set HF_HOME=/data/.huggingface for caching.

- spaces-zerogpu.md
  - ZeroGPU only for Gradio SDK.
  - Use @spaces.GPU decorator to acquire/release GPU per call.
  - duration parameter improves queue priority; supports dynamic duration callable.
  - No torch.compile; AOT compile with torch 2.8+.
  - Daily quota tiers affect queue priority.

- spaces-sdks-docker.md
  - Secrets/variables management for Docker (build-time secret mount).

## Suggested rg patterns

- Secrets/variables: rg -n "Managing secrets|variables|environment" spaces-overview.md
- ZeroGPU duration: rg -n "Duration Management|dynamic duration|@spaces.GPU" spaces-zerogpu.md
- Persistent storage: rg -n "Persistent storage|/data|HF_HOME" spaces-storage.md
- README YAML: rg -n "Spaces Configuration Reference|sdk|app_file" spaces-config-reference.md
- Dependencies: rg -n "requirements.txt|packages.txt|pre-requirements" spaces-dependencies.md
