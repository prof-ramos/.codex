---
name: telegram-bot-performance-engineer
description: This skill should be used when analyzing, profiling, or optimizing Telegram bots built with Python/Telethon, especially for performance bottlenecks, rate limits, caching, API usage, or when the user asks for a full repo review or best practices.
tools:
  - Read
  - Write
  - Edit
  - Bash
model: opus
---

# Telegram Bot Performance Engineer

## Overview
Habilitar analise tecnica e otimizacao de desempenho para bots do Telegram com Python/Telethon, cobrindo profiling, rate limits, caching e uso eficiente da API.

## Quando usar
Usar esta skill quando o usuario pedir:
- "Verifique o meu repositorio completo" (esperar analise ampla de bibliotecas e melhores praticas).
- "Analise esse Bot do Telegram".
- "Melhore esse bot".
- "Aplique as melhores praticas no Bot".
- "Crie um bot para Telegram".

## Workflow principal
1) Confirmar objetivo e escala
- Perguntar volume (usuarios, mensagens/dia), limites de latencia e custos aceitaveis.
- Definir ambiente (local, servidor, worker, cron) e requisitos de confiabilidade.

2) Mapear o repositorio
- Localizar pontos de entrada, handlers e loops assync (ex.: `main.py`, `bot.py`, `handlers/`).
- Inventariar dependencias via `pyproject.toml` e `uv.lock`.
- Se o usuario pedir analise completa, consultar docs com Context7:
  - Resolver o ID da lib com `resolve-library-id`.
  - Buscar docs focadas em performance e rate limit com `get-library-docs`.
  - Priorizar Telethon e libs de IO/queue/cache encontradas no repo.

3) Medir e achar gargalos
- Coletar logs e tempos com `time.perf_counter` nos fluxos criticos.
- Preferir `cProfile`/`py-spy` para CPU e `tracemalloc` para memoria.
- Identificar N+1 chamadas, loops com chamadas remotas e IO bloqueante.

4) Mitigar rate limits e uso excessivo da API
- Tratar `FloodWaitError` com backoff e jitter.
- Ajustar `flood_sleep_threshold` no `TelegramClient` quando aplicavel.
- Limitar concorrencia com `asyncio.Semaphore` e processar em lotes.

5) Aplicar caching e reduzir chamadas repetidas
- Reaproveitar entidades/peers ja resolvidos; evitar `get_entity` em loops.
- Introduzir cache TTL para resultados frequentes (usuarios, chats, configs).
- Persistir dados derivados quando custo de recomputacao for alto.

6) Validar melhorias
- Reexecutar medidas e comparar antes/depois.
- Documentar impacto (latencia, throughput, chamadas, memoria).

## Saidas esperadas
- Entregar um resumo com: gargalos, mudancas propostas, riscos e prioridade.
- Incluir plano de implementacao com passos curtos e metricas de sucesso.
- Sugerir testes e observabilidade minima para garantir regressao zero.

## Recursos
Consultar `references/telethon-performance-playbook.md` para checklist detalhado.
