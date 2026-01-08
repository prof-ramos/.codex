---
name: rag-auditor
description: Produzir auditoria de colapso semantico em RAG, taxonomia hierarquica e schema de Graph-RAG para sistemas de recuperacao. Usar quando o usuario pede diagnostico de alucinacao/queda de precisao em vector stores, arquitetura RAG hierarquica ou grafo de conhecimento.
---

# Rag Auditor

## Visao Geral

Gerar tres entregaveis em cadeia para sistemas RAG: relatorio de risco de colapso semantico, taxonomia hierarquica de recuperacao e schema de knowledge graph. Produzir saidas completas em PT-BR com formato Markdown e secoes fixas.

## Fluxo de Trabalho (3 Passos)

### Passo 1: Auditoria de Colapso Semantico

1. Coletar inputs minimos: numero total de documentos/chunks, dominio/industria, modelo de embedding (ou "Standard"), comprimento medio (se o usuario souber) e 2-3 exemplos de documentos.
2. Se algum dado estiver ausente, pedir apenas o necessario para calcular o relatorio. Caso o comprimento medio nao seja informado, assumir 800 tokens e declarar a suposicao.
3. Calcular o risco usando o guia em `references/heuristics.md`.
4. Redigir o relatorio com tom brutalista e direto, focado em falha estrutural e maldicao da dimensionalidade.

### Passo 2: Taxonomia Hierarquica

1. Usar o dominio e 2-3 perguntas tipicas do usuario.
2. Criar uma arvore com 3 niveis (Root -> Branch -> Leaf) e categorias mutuamente exclusivas.
3. Explicar a logica de roteamento (classificador simples por sinais/termos ou roteador LLM).
4. Demonstrar reducao do espaco de busca com um calculo simples (bucket_size = total_docs / (roots * branches)).

### Passo 3: Schema Graph-RAG

1. Extrair entidades principais (substantivos) a partir da hierarquia do Passo 2.
2. Definir tipos de nodes e edges com nomes consistentes e verbos claros.
3. Simular uma travessia de grafo com uma consulta real do usuario.
4. Manter tom engenheirado e deterministico.

## Regras de Formato e Estilo

- Idioma: PT-BR.
- Formato: Markdown com titulos e listas.
- Emojis funcionais nas secoes, conforme os modelos abaixo.
- Nao usar placeholders. Se um dado faltar, solicitar antes de gerar.
- Manter cada passo autocontido e coerente com o anterior.

### Formatos obrigatorios

**Passo 1**
```
# 🚨 RELATORIO DE RISCO DE COLAPSO SEMANTICO

## 📊 ESTATISTICAS VITAIS
- **Volume Atual:** [Valor]
- **Queda de Precisao Projetada:** [Estimativa]
- **Pontuacao de Probabilidade de Colapso:** [0-100%]

## 📉 O PRECIPICIO DE PRECISAO
[Explicacao objetiva do ponto de quebra]

## 🧠 A ARMADILHA DA ALUCINACAO
[Analise especifica do dominio]

## 🛠 INTERVENCAO RECOMENDADA
[Preview curto de hierarquia/grafo]
```

**Passo 2**
```
## 🌳 A ESTRATEGIA DE INDICE HIERARQUICO

### NIVEL 1: ROOT NODES (Os Porteiros)
[Lista]

### NIVEL 2: BRANCH NODES (Os Filtros)
[Detalhamento por root]

### 🧭 LOGICA DE ROTEAMENTO
[Como a query escolhe caminho]

### 📉 REDUCAO DO ESPACO DE BUSCA
[Calculo simples e reducao]
```

**Passo 3**
```
## 🕸️ SCHEMA DE KNOWLEDGE GRAPH

### 🟢 TIPOS DE NODE (As "Coisas")
- **[Node]**: [Descricao]

### 🔗 TIPOS DE EDGE (As "Conexoes")
- **[Edge]**: [Descricao]

### 🛣️ SIMULACAO DE TRAVESSIA
**Consulta:** "[Pergunta]" **Caminho:** [Node A] --(Edge)--> [Node B] --(Edge)--> [Resposta]
```

## Recursos

- `references/heuristics.md`: Heuristicas para calcular limiar de ruido, precipicio de precisao e pontuacao de colapso.
