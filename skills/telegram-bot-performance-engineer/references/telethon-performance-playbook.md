# Telethon Performance Playbook

## Triage rapido
- Definir volume de atualizacoes (updates por minuto) e picos esperados.
- Medir latencia alvo por comando e tempo total de processamento.
- Identificar fontes de carga externa (API externa, banco, filesystem).

## Profiling e medicao
- Medir trechos criticos com `time.perf_counter` e log estruturado.
- Usar `cProfile` para hotspots de CPU e `tracemalloc` para memoria.
- Preferir amostragem com `py-spy` quando o overhead de profiling for um problema.
- Registrar contagem de chamadas Telegram e tempo medio por request.

## Rate limits e estabilidade
- Tratar `FloodWaitError` com backoff exponencial e jitter.
- Configurar `flood_sleep_threshold` no `TelegramClient` para auto-sleep seguro.
- Evitar concorrencia ilimitada; aplicar `asyncio.Semaphore` ou filas.
- Agrupar chamadas remotas em lotes, quando possivel.

## Caching
- Reutilizar entidades e peers resolvidos para evitar repeticao de `get_entity`.
- Manter cache TTL para dados estaveis (usuarios, chats, configs).
- Persistir resultados caros em disco quando adequado (ex.: estatisticas).

## Uso eficiente da API
- Preferir iteradores (`iter_*`) para streaming em vez de carregar tudo em memoria.
- Evitar chamadas repetidas em loops; armazenar resultados intermediarios.
- Reduzir chamadas redundantes em handlers com debounce/ratelimit interno.

## Concorrencia e async
- Limitar `gather` em listas grandes; processar em batches.
- Separar CPU-bound em `run_in_executor` quando bloquear o event loop.
- Evitar IO bloqueante no caminho critico; usar libs async.

## Validacao
- Reexecutar o mesmo fluxo com metricas comparaveis (antes/depois).
- Registrar ganhos esperados: latencia, throughput, chamadas, memoria.
- Documentar riscos e estrategia de rollback.
