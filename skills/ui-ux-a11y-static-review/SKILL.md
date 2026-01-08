---
name: ui-ux-a11y-static-review
description: This skill should be used when performing static UI/UX and accessibility reviews of frontend codebases and producing a three-step report (context mapping, violations, executive synthesis) from code only.
---

# UI UX A11y Static Review

## Overview

Gerar revisoes estaticas de UI/UX e acessibilidade em tres etapas (mapeamento, validacao e sintese), com base apenas em codigo e arquivos fornecidos.

## Quando usar

- Usar quando o usuario pedir revisao de UI/UX, acessibilidade ou conformidade baseada em analise estatica de frontend.
- Usar quando o usuario solicitar um relatorio em etapas (mapeamento, validacao e sintese).
- Evitar quando o pedido exigir execucao de app, testes visuais, navegador ou auditoria dinamica.

## Workflow (3 prompts)

### Passo 1 - Descoberta e mapeamento

- Carregar `references/prompt-1.md`.
- Mapear estrutura, stack de UI, tokens/tema e componentes relevantes com base nos arquivos visiveis.
- Produzir a resposta no formato exigido pelo prompt (tabelas e secoes).

### Passo 2 - Validacao estatica de regras

- Confirmar que o resultado do Passo 1 foi fornecido; solicitar se estiver ausente.
- Carregar `references/prompt-2.md`.
- Reportar apenas violacoes, riscos e pontos de atencao com evidencia estatica.
- Entregar uma unica tabela Markdown no formato especificado pelo prompt.

### Passo 3 - Sintese e relatorio executivo

- Confirmar que a tabela do Passo 2 foi fornecida; solicitar se estiver ausente.
- Carregar `references/prompt-3.md`.
- Produzir resumo executivo, problemas por categoria, sugestoes de padronizacao com snippet critico e backlog priorizado.

## Regras gerais

- Executar analise estritamente estatica; nao rodar codigo, nao simular navegador, nao inferir layout.
- Usar apenas arquivos explicitamente mostrados; pedir acesso quando faltar contexto.
- Omitir pontos sem evidencia clara no codigo.
- Responder em portugues e manter tom tecnico e objetivo.

## Recursos

- `references/prompt-1.md`
- `references/prompt-2.md`
- `references/prompt-3.md`
