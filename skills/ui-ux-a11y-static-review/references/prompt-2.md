# PROMPT 2 - VALIDACAO ESTATICA DE REGRAS

Voce continua como revisor(a) senior de UI/UX e Acessibilidade.

Agora, com base no mapeamento ja feito antes, sua tarefa e identificar violacoes e riscos, de forma objetiva.

IMPORTANTE - CONTEXTO ANTERIOR
Antes deste prompt, foi gerado um mapeamento de stack e componentes.
Cole aqui a saida do Prompt 1:

`[[COLE AQUI O RESULTADO DO MAPEAMENTO DO PROMPT 1]]`

AVISO - Regras fundamentais deste passo
- Analise estritamente estatica: trabalhe apenas com o codigo mostrado.
- Nao tente simular layout pixel-perfect - foque em evidencias claras:
  - propriedades CSS/utility classes,
  - estrutura JSX/HTML,
  - tokens e tema.
- Management by Exception:
  - Liste apenas violacoes, riscos e pontos de atencao.
  - Nao liste locais onde a implementacao parece correta.
- Se algo nao pode ser inferido estaticamente, simplesmente nao reporte.

---

## 1. Regras de referencia (resumo operacional)

Concentre-se em encontrar:

- Violacao explicita: ex. `outline: none` sem foco alternativo.
- Ausencia de atributo obrigatorio: ex. botao implementado como `<div>` sem role/teclado.
- Configuracao problematica de tokens: ex. tokens de botao pequenos demais por padrao.

### 1.1. Tamanho de botoes e alvos de toque

- Touch target minimo em mobile approx 44x44 px (iOS) / 48x48 px (Android).

- Conversao de unidades (para checagem aproximada):
  - Assuma `1rem = 16px` (base) a menos que o codigo indique outro root `font-size`.
  - Para Tailwind, assuma:
    - `1 unidade de spacing = 0.25rem = 4px`
      (ex.: `h-10` approx 40px, `h-12` approx 48px).
- Validacao:
  - Alerte se botoes padrao/primarios usam alturas claramente inferiores a ~44px
    (ex.: `h-8`, `py-1` com `text-sm`, etc.).
  - Verifique `padding` vertical: botoes so com `py-1` ou `py-2` frequentemente produzem alvos muito pequenos.

### 1.2. Espacamentos e grid

- Verificar se existe um sistema coerente de spacing (multiplos de 4/8).
- Procurar por:
  - Valores "avulsos" e inconsistentes (ex.: `margin: 13px; padding: 7px;` sem relacao com tokens).
  - Cards / containers principais sem padding interno minimo.
  - Gaps extremamente pequenos entre botoes/inputs criticos (risco de clique acidental).

### 1.3. Hierarquia de botoes & contraste basico

- Identificar:
  - Botao primario (cor de destaque, preenchido).
  - Botao secundario (outline/ghost).
- Verificar:
  - Se tokens de cor para botao primario e texto (`onPrimary`, etc.) sugerem bom contraste.
  - Uso de textos claros sobre fundos muito claros, ou escuros sobre fundos muito escuros (suspeita de baixa razao de contraste).

### 1.4. Teclado, foco e semantica basica

Procure especificamente por:

- Uso de elementos nao semanticos:
  - `onClick` em `div` ou `span` para acoes -> violacao; preferir `button`.
- Remocao de foco:
  - CSS com `outline: none` ou `outline: 0` sem substituicao clara (`box-shadow`, `border`, etc.).
- Botoes em formularios:
  - Falta de `type="button"` em botoes que nao deveriam submeter o formulario.

### 1.5. Formularios e labels

- Inputs devem ter:
  - `<label>` associado (`for`/`id`) ou `aria-label`/`aria-labelledby`.
- Campos obrigatorios:
  - Se usam `required`, ver se ha indicacao textual (nao so cor).
- Erros:
  - Verificar se ha padrao de mensagem de erro reutilizavel (`ErrorMessage`, `aria-describedby`).

### 1.6. Estrutura semantica e ARIA

- Titulos:
  - Evitar uso de `div` para titulos onde `h1-h3` seria mais adequado.
- Elementos interativos:
  - Links (`<a>`) devem navegar; acoes internas devem ser `button`.
- ARIA:
  - `role="button"` em elementos nao nativos sem handlers de teclado (`Enter`/`Space`) e um risco.
  - Evitar ARIA redundante ou incorreta que conflita com o nativo.

### 1.7. Motion e prefers-reduced-motion

- Procurar por:
  - Animacoes/transicoes aplicadas de forma extensa (`animation`, `transition` em grandes blocos).
- Verificar se:
  - Existe alguma consideracao de `@media (prefers-reduced-motion: reduce)` em projetos com animacao relevante.

---

## 2. O que voce deve PRODUZIR neste passo

### 2.1. Apenas violacoes e riscos

Para cada categoria (botoes, espacamentos, tipografia, etc.):

- Liste apenas:
  - Violacoes claras.
  - Oportunidades de melhoria com impacto relevante.

### 2.2. Formato da saida

Use uma unica tabela Markdown com o formato:

| Categoria       | Arquivo e local aproximado                  | Descricao da violacao / risco                                  | Regra relacionada                         | Sugestao concreta de correcao                          |
|----------------|----------------------------------------------|-----------------------------------------------------------------|-------------------------------------------|--------------------------------------------------------|
| Botoes         | `src/components/ui/Button.tsx` (linha ~45)   | Botao primario com `py-1` e `text-sm`, alvo de toque reduzido. | Tamanho minimo de alvos de toque          | Aumentar padding vertical (`py-2`/`py-3`) e fonte >=14 |
| Acessibilidade | `src/components/Card.tsx` (linha ~30)        | Usa `<div onClick={...}>` em vez de `<button>`.                | Semantica e acessibilidade de teclado     | Trocar por `<button>` ou adicionar role + key handlers |

Regras:

- Se nao ha evidencia clara de violacao, nao coloque nada na tabela.
- Voce pode consolidar padroes recorrentes:
  - Ex.: "Este problema aparece em `Button`, `IconButton` e `SecondaryButton`."

---

## 3. Tom e escopo

- Fale de forma tecnica e objetiva, direto ao ponto.
- Nao explique conceitos basicos (WCAG, o que e um botao primario).
- Foque em diagnostico acionavel: "o que esta errado + como corrigir".

--------------------------------------------
# FIM DO PROMPT 2
--------------------------------------------
