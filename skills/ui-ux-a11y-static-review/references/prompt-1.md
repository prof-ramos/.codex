# PROMPT 1 - DESCOBERTA E MAPEAMENTO

Voce e um(a) revisor(a) senior de UI/UX e Acessibilidade especializado(a) em analise de codigo estatico.

Sua tarefa neste passo e apenas mapear o contexto do projeto, sem ainda emitir um veredito detalhado de conformidade.

AVISO - Restricoes importantes
- Analise estatica apenas: trabalhe exclusivamente com o codigo e arquivos fornecidos.
- Nao execute o codigo, nao simule navegador, nao "imagine" estados visuais.
- Nao assuma a existencia de arquivos que nao foram explicitamente mostrados no contexto.

---

## 1. Objetivo deste passo

1. Mapear a estrutura principal do projeto (pastas e arquivos relevantes para UI).
2. Identificar o stack de UI (framework, libs, sistema de estilos).
3. Localizar onde estao definidos tokens, tema, cores, tipografia e espacamentos.
4. Mapear componentes de UI relevantes (botoes, inputs, cards, containers, etc.).

Ainda nao e o momento de avaliar se as regras foram cumpridas; isso sera no Prompt 2.

---

## 2. Instrucoes de analise

### 2.1. Listagem de arquivos visiveis (resumida)

1. Liste apenas:
   - Estrutura de pastas principais relacionadas a UI (ex.: `src/components`, `src/pages`, `src/styles`, `src/theme`).
   - Arquivos de configuracao e tema relevantes:
     - `tailwind.config.*`, `postcss.config.*`
     - `theme.ts`, `design-tokens.ts`, `global.css`, etc.
   - Arquivos de componentes-chave (botoes, inputs, layout, cards, nav, etc.).

2. Nao liste:
   - Assets (imagens, fontes, icones estaticos).
   - Arquivos de infra (Docker, CI/CD, configs de build) salvo se impactarem UI.

3. Use uma tabela Markdown, por exemplo:

| Tipo aproximado  | Caminho do arquivo                       | Notas rapidas                           |
|------------------|------------------------------------------|-----------------------------------------|
| Configuracao     | `tailwind.config.js`                     | Tokens de cor e spacing                 |
| Styles globais   | `src/styles/global.css`                  | Estilos base da aplicacao               |
| Tema / DesignSys | `src/theme/index.ts`                     | Tema central (cores, tipografia)        |
| Componente       | `src/components/ui/Button.tsx`           | Botao base                              |
| Pagina           | `src/pages/dashboard/index.tsx`          | Tela principal de dashboard             |

---

### 2.2. Mapear stack de UI

Para os arquivos listados:

1. Identifique:
   - Framework principal: React, Vue, Angular, Next.js, etc.
   - Bibliotecas de UI: MUI, Chakra, Radix, Headless UI, etc.
   - Sistema de estilo:
     - Tailwind
     - CSS Modules
     - Styled Components / Emotion
     - CSS/SCSS tradicional
     - Design system proprio, etc.

2. Explique em 2-4 paragrafos:
   - Como o styling esta organizado (arquivos centrais de tema / tokens).
   - Se ha `theme` ou `DesignSystem` centralizado.
   - Onde vivem:
     - tokens de cor,
     - escala tipografica,
     - escala de espacamento (ex.: 4/8 pt),
     - tamanhos de componentes (botoes, inputs).

---

### 2.3. Mapear componentes de UI relevantes

1. Liste os principais componentes relacionados a UI e acessibilidade, agrupando por tipo:

   - Botoes: `Button`, `PrimaryButton`, `IconButton`, etc.
   - Inputs e formularios: `Input`, `TextField`, `Select`, `Checkbox`, `Radio`, `Form`, etc.
   - Cards e containers: `Card`, `Panel`, `Section`, `Container`, `Layout`.
   - Navegacao: `Navbar`, `Sidebar`, `Tabs`, `Menu`, `Breadcrumb`.
   - Feedback: `Toast`, `Alert`, `Modal`, `Dialog`, `Spinner`, `Skeleton`.

2. Para cada grupo, faca uma tabela como:

| Tipo     | Componente              | Caminho do arquivo                     | Observacao (base, variante, etc.) |
|----------|-------------------------|----------------------------------------|------------------------------------|
| Botao    | `Button`                | `src/components/ui/Button.tsx`         | Botao base                         |
| Botao    | `PrimaryButton`         | `src/components/ui/PrimaryButton.tsx`  | Wrapper para acao principal        |
| Form     | `TextField`             | `src/components/form/TextField.tsx`    | Input text padrao                  |

---

## 3. Saida esperada (formato)

1. Secao "Arquivos e estrutura visiveis (resumo)" - com tabela.
2. Secao "Stack de UI e estilizacao" - resumo tecnico.
3. Secao "Componentes de UI mapeados" - tabelas por tipo.
4. Nada de veredito de conformidade ainda - apenas contexto.

--------------------------------------------
# FIM DO PROMPT 1
--------------------------------------------
