---
name: en-ptbr-tech-md
description: This skill should be used when translating English technical content to Brazilian Portuguese with Markdown output, preserving structure and terminology.
---

# en-ptbr-tech-md

## Purpose

Fornecer um fluxo de traducao tecnica de ingles para PT-BR com saida em Markdown, mantendo naturalidade, precisao e uso consagrado de termos tecnicos.

## When to use

Usar quando o pedido envolver traducao de conteudo em ingles para PT-BR com foco tecnico (software, infraestrutura, dados, marketing digital, blogs tecnologicos) e a saida precisar estar em Markdown.

## Workflow

### 1) Preparar contexto

- Identificar dominio, publico-alvo e nivel de formalidade do texto.
- Identificar estrutura original: titulos, listas, tabelas, citacoes, blocos de codigo e enfases.
- Carregar `references/glossary.md` para termos tecnicos mantidos em ingles.

### 2) Traduzir com criterio terminologico

- Manter em ingles termos tecnicos consagrados (ver `references/glossary.md`).
- Traduzir termos com equivalente natural em PT-BR quando houver uso comum e claro.
- Priorizar naturalidade e clareza, evitando traducoes literais artificiais.

### 3) Converter e preservar estrutura em Markdown

- Converter titulos para `#`, `##`, `###` conforme hierarquia.
- Converter listas para `-` ou `1.` conforme o caso.
- Preservar tabelas com `|` e alinhamento simples.
- Manter codigo inline com crase simples e blocos com triplas crases e linguagem quando identificavel.
- Nao traduzir conteudo de codigo; traduzir apenas comentarios claramente identificados.

### 4) Saida limpa

- Retornar somente a traducao final em Markdown.
- Evitar explicacoes, observacoes ou textos extras fora da traducao.

## Output rules

- Sempre produzir Markdown, mesmo quando a entrada nao estiver estruturada.
- Converter destaques implicitos (ex.: "Summary") em titulos equivalentes quando for claro.
