# Heuristicas de Colapso Semantico

Usar estas regras para estimar limiar de ruido, precipicio de precisao e probabilidade de colapso. Ajustar apenas se o usuario fornecer dados empiricos.

## Variaveis

- `D`: total de documentos ou chunks.
- `L`: comprimento medio em tokens. Se ausente, assumir 800 tokens.
- `dim`: dimensionalidade do embedding.
- `S`: fator de especificidade do dominio.
- `F_L`: fator de comprimento.

## Dimensao (dim)

- `text-embedding-3-small`: 1536
- `text-embedding-3-large`: 3072
- `openai-ada-002`: 1536
- Desconhecido/"Standard": 1536

## Fatores

**S (especificidade do dominio)**
- Alta (jurisprudencia muito especializada, codigo interno, medicina ultra-especifica): 1.4
- Media (setores comuns com jargoes, ex: RH, suporte tecnico): 1.0
- Baixa (conteudo generalista ou multimodal, marketing amplo): 0.7

**F_L (comprimento medio)**
- `L` <= 400: 1.1
- 401-1000: 1.0
- 1001-2000: 0.8
- >2000: 0.6

## Limiar de Ruido / Precipicio de Precisao

Calcular:

`T = 10_000 * (1536 / dim) * S * F_L`

Interpretacao:
- `D < 0.5T`: risco baixo
- `0.5T <= D < 0.8T`: risco moderado
- `0.8T <= D < T`: risco alto
- `T <= D < 1.5T`: risco muito alto
- `D >= 1.5T`: colapso quase certo

## Pontuacao de Probabilidade de Colapso

Mapear `R = D / T`:
- `R < 0.5` -> 15%
- `0.5 <= R < 0.8` -> 35%
- `0.8 <= R < 1.0` -> 60%
- `1.0 <= R < 1.5` -> 80%
- `R >= 1.5` -> 95%

Adicionar +5% se o embedding for desconhecido/"Standard".
Limitar entre 5% e 99%.

## Queda de Precisao Projetada

Usar faixa baseada em `R`:
- `R < 0.5`: 10-20%
- `0.5 <= R < 0.8`: 25-40%
- `0.8 <= R < 1.0`: 45-60%
- `1.0 <= R < 1.5`: 65-80%
- `R >= 1.5`: 80-92%

## Vetor de Alucinacao (explicacao)

Construir texto curto explicando:
- Densificacao: pontos tornam-se quase equidistantes na hiperesfera.
- Overlap semantico: documentos longos e generalistas geram embeddings "mistos".
- Top-k ruidoso: aumentar contexto adiciona falsos positivos e confunde o modelo.

## Intervencao Recomendada (preview)

Sugerir migracao para:
- Roteamento hierarquico (Passo 2).
- Graph-RAG para relacoes deterministicas (Passo 3).

Manter 2-3 frases, sem prescricao detalhada.
