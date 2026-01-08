---
name: hf-spaces-expert
description: This skill should be used when creating or configuring Hugging Face Spaces, including ZeroGPU hardware, secrets/env variables, persistent storage, repo-based deploys, and build/memory troubleshooting.
---

# Hf Spaces Expert

## Overview

Criar e ajustar Spaces do Hugging Face com foco em operacoes praticas (arquivos de app, dependencias, README) e otimizacao para workloads pesados em ZeroGPU.

## Fluxo principal (workflow)

### 1) Coletar contexto minimo

- Confirmar SDK (preferir Gradio para ZeroGPU) e nome do Space/repo.
- Confirmar necessidade de ZeroGPU, Storage persistente e Secrets/Env.
- Confirmar entradas/saidas principais do app e tamanho tipico dos PDFs.
- Identificar limites de tempo de execucao por job e requisitos de concorrencia.

### 2) Configurar README.md (YAML)

- Escrever o bloco YAML do README.md com `sdk`, `app_file`, `python_version`, `sdk_version` e `title`.
- Definir `suggested_hardware` e `suggested_storage` quando quiser orientar duplicacoes.
- Ajustar `startup_duration_timeout` quando o boot inicial for pesado.
- Usar `preload_from_hub` quando modelos/arquivos grandes precisarem baixar no build.

Exemplo minimo (adaptar):

```yaml
---
title: Docling Space
emoji: ":page_facing_up:"
colorFrom: blue
colorTo: green
sdk: gradio
app_file: app.py
python_version: 3.10
sdk_version: 4.44.1
suggested_hardware: "cpu-basic"
suggested_storage: "small"
startup_duration_timeout: 45m
---
```

### 3) Configurar dependencias

- Declarar pacotes Python em `requirements.txt`.
- Usar `pre-requirements.txt` se precisar atualizar pip/compiladores antes.
- Usar `packages.txt` para dependencias Debian (ex.: libs de imagem/PDF).

### 4) Implementar/ajustar `app.py`

- Estruturar processamento de PDF em etapas curtas e isoladas.
- Reduzir uso de memoria com:
  - Processamento por paginas/lotes.
  - Liberacao explicita de objetos grandes.
  - Escrita de artefatos intermediarios em `/data` quando houver storage persistente.
- Controlar concorrencia para evitar OOM:
  - Limitar workers e tamanho de fila no Gradio.
  - Evitar processar multiplos PDFs longos em paralelo.

### 5) ZeroGPU e gestao de filas

- Usar `@spaces.GPU` para funcoes GPU-bound.
- Definir `duration` para otimizar prioridade de fila.
- Implementar duracao dinamica baseada no tamanho do PDF (paginas, MB, etc.).
- Evitar `torch.compile`; preferir AOT se necessario.

Exemplo de duracao dinamica (adaptar ao fluxo real):

```python
import spaces

def duration_from_pages(pages_count: int) -> int:
    base = 30
    per_page = 2
    return base + per_page * pages_count

@spaces.GPU(duration=duration_from_pages)
def process_pdf(file_path: str, pages_count: int):
    ...
```

### 6) Secrets/Env e Storage persistente

- Criar variaveis e secrets no Settings do Space; evitar hard-code.
- Ler variaveis com `os.getenv` (Gradio/Spaces padrao).
- Quando houver storage persistente:
  - Usar `/data` para cache e outputs.
  - Definir `HF_HOME=/data/.huggingface` para evitar downloads repetidos.

### 7) Deploy por repositorio

- Manter `app.py`, `requirements.txt`, `README.md` na raiz do repo.
- Lembrar que cada `git push` dispara rebuild.
- Documentar no README instrucoes de uso e limites conhecidos (ex.: tamanho maximo de PDF).

### 8) Troubleshooting (build/memoria)

- Build falhando: validar `requirements.txt`, `pre-requirements.txt`, `packages.txt`.
- Timeouts de startup: ampliar `startup_duration_timeout` no YAML.
- OOM: reduzir concorrencia, baixar batch size, usar `/data` para evitar memoria RAM.
- ZeroGPU lento: diminuir `duration` quando possivel e reduzir cargas GPU por job.

## Recursos

- Referencia oficial local: `references/hf_spaces_docs.md`
  - Usar para checar fatos especificos sobre ZeroGPU, Storage, Secrets/Env e YAML do README.
