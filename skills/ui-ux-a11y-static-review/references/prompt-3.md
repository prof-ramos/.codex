# PROMPT 3 - SINTESE E RELATORIO EXECUTIVO

Agora voce recebera como entrada:

- (Opcional) O contexto do projeto / stack (saida do Prompt 1).
- A tabela de violacoes e riscos produzida no Prompt 2.

Seu papel continua sendo de revisor(a) senior de UI/UX e Acessibilidade, agora focado em sintese, priorizacao e direcionamento para o time.

---

## 1. Objetivo

Transformar a lista de violacoes em um relatorio executivo e um plano de acao, com:

1. Resumo geral de conformidade.
2. Principais problemas por categoria.
3. Sugestoes de padronizacao (incluindo snippet critico).
4. Backlog priorizado por impacto (P0, P1, P2).

---

## 2. Estrutura da resposta

### 2.1. Resumo geral

- Classifique o estado geral como, por exemplo:
  - "Altamente problematico"
  - "Parcialmente conforme, com riscos criticos"
  - "Majoritariamente conforme, com melhorias pontuais"
- Em 2-3 paragrafos, explique:
  - Pontos fortes do sistema (onde ha boas praticas claras).
  - Riscos mais importantes (principalmente acessibilidade e UX de fluxo).

---

### 2.2. Problemas por categoria (visao consolidada)

Monte uma lista por categoria, consolidando os padroes encontrados:

- Acessibilidade (P0)
  - Ex.: Uso recorrente de `div` clicavel em vez de `button` em componentes de acao.
- Formularios (P0/P1)
  - Ex.: Inputs sem label associado e sem `aria-*`.
- Espacamentos / grid (P1/P2)
  - Ex.: Falta de padrao 4/8pt e uso de valores "aleatorios".
- Motion & foco (P0/P1)
  - Ex.: `outline: none` sem estilo de foco alternativo.

Voce nao precisa repetir todos os arquivos da tabela original, apenas:

- Descrever o padrao de problema.
- Citar exemplos representativos (1-3 por categoria).

---

### 2.3. Sugestoes de padronizacao

Liste recomendacoes em formato de bullet points, por exemplo:

- Criar um componente padrao de botao com:
  - Tamanhos pre-definidos (`sm`, `md`, `lg`) atrelados a tokens de spacing.
  - Estilo de foco visivel consistente entre todos os botoes.
  - Variantes primaria/ secundario/terciaria com tokens de cor bem definidos.

- Centralizar tokens de:
  - Espacamento (base em multiplos de 4/8pt).
  - Tipografia (escala e pesos).
  - Cores (incluindo `on-*` para contraste).

- Definir convencoes para:
  - Labels, placeholders e mensagens de erro em formularios.
  - Uso de elementos semanticos (`button`, `a`, `nav`, `header`, etc.).
  - Animacoes e respeito a `prefers-reduced-motion`.

#### 2.3.1. Snippet obrigatorio para o problema mais critico (P0)

- Identifique a violacao P0 mais critica (ex.: botao sem foco visivel / `div` clicavel).
- Forneca um snippet de codigo que demonstre uma solucao padrao, por exemplo:

  - Exemplo de `Button` acessivel (React/Tailwind ou stack do projeto).
  - Exemplo de configuracao de token em `tailwind.config.js` ou arquivo de tema.

O snippet deve ser pragmatico, pronto para ser usado como base pelo time.

---

### 2.4. Backlog priorizado

Monte uma tabela de backlog:

| Prioridade | Tipo de problema      | Descricao resumida                         | Impacto principal                        |
|-----------|------------------------|--------------------------------------------|------------------------------------------|
| P0        | Acessibilidade critica | `div` clicaveis no lugar de `button`       | Teclado / leitores de tela               |
| P0        | Foco                   | `outline: none` sem foco alternativo       | Usuarios de teclado / baixa visao        |
| P1        | Formularios            | Inputs sem label associado                 | Compreensao / leitores de tela           |
| P1        | Hierarquia visual      | Botoes primarios pouco diferenciados       | Tomada de decisao e fluxo de tarefas     |
| P2        | Consistencia visual    | Espacamentos fora da escala 4/8 pt         | Coesao visual e percepcao de qualidade   |

Regra:

- P0: afeta acessibilidade basica (teclado, foco, contraste, semantica critica).
- P1: afeta UX de leitura, formularios, hierarquia visual, mas nao bloqueia uso.
- P2: refino visual e consistencia estetica.

---

## 3. Estilo da resposta

- Fale como um(a) senior se reportando para lideres de produto/engenharia.
- Traga clareza de impacto (quem e afetado, em quais cenarios).
- Foque em decisoes acionaveis: o que deve ser ajustado primeiro e por que.

--------------------------------------------
# FIM DO PROMPT 3
--------------------------------------------
