---
name: pauta-mensal
description: >
  Organiza a grade completa de conteúdo do mês pra um cliente (feed semanal +
  stories diários + sugestão de destaques), cruzando sazonalidade, recomendações
  do ciclo anterior e a rotação de temas recorrentes por dia da semana. Gera saída
  em markdown (leitura/aprovação) e em planilha .xlsx (formato usado
  historicamente pelo cliente). Use quando o usuário disser "monta a pauta do mês",
  "grade de conteúdo de [mês]", "o que a gente posta esse mês", ou pedir o
  planejamento mensal de um cliente.
---

# /pauta-mensal — Grade de Conteúdo do Mês

## Dependências

- **Contexto do cliente:** `clientes/<cliente>/AGENTS.md` (tom, canais, sazonalidade)
- **Briefing completo:** `clientes/<cliente>/briefing.md` (sob demanda, se precisar de detalhe)
- **Identidade visual:** `clientes/<cliente>/marca/design-guide.md`
- **Histórico de recomendações:** `clientes/<cliente>/analises/recomendacoes.md`
  (o que `/analisar-dados` recomendou no ciclo anterior — a pauta deve refletir isso)
- **Tom de voz da operação:** `_contexto/preferencias.md`
- **Rotação de temas:** `references/temas-recorrentes.md` (nesta pasta)
- **Formato de saída:** `references/formato-planilhas.md` (nesta pasta)

---

## Workflow

### Passo 1 — Definir o mês e o cliente

Se não estiver claro pela conversa, perguntar:
- "Pauta de qual cliente e qual mês?"

### Passo 2 — Reunir os insumos

1. Ler `clientes/<cliente>/AGENTS.md` pra relembrar canais ativos, tom e calendário
   de sazonalidade (datas comemorativas + datas espelhadas de marketplace).
2. Ler `clientes/<cliente>/analises/recomendacoes.md` (se existir) pra saber o que
   foi recomendado no ciclo anterior e que ainda não virou pauta.
3. Verificar se há produto(s) em destaque do mês definido (estoque alto, promoção,
   sazonalidade). Se não estiver claro, perguntar: "Tem algum produto que deveria
   ser o destaque desse mês?"

### Passo 3 — Montar a grade de Publicações (feed semanal)

Uma linha por semana do mês (Sem 1, Sem 2, Sem 3, Sem 4, e Sem 5 se o mês tiver).
Cada linha cruza:
- Datas comemorativas relevantes daquela semana
- O produto em destaque do mês (reforçado especialmente nas primeiras semanas)
- Recomendações pendentes do ciclo anterior

Preencher pra cada semana: Tema, Produto(s), Utilidade/Abordagem, Orientação para
criação (isso vira o input direto do `/roteiro-post` depois), Materiais Adicionais
(Story, Banner, etc.), Orientações Gerais.

### Passo 4 — Montar a grade de Stories (diária)

Usar `references/temas-recorrentes.md` como base de rotação por dia da semana.
Pra cada dia do mês, definir o tema (seguindo a tendência do dia) e uma descrição
específica do que postar naquele dia, considerando o produto destaque e a
sazonalidade da semana. Deixar a coluna de retorno/métricas em branco.

### Passo 5 — Revisar Destaques

Comparar a lista de destaques fixos sugeridos (`temas-recorrentes.md`) com o que já
existe no perfil do cliente (perguntar se não souber). Só sugerir mudança se algo
novo justificar (ex: nova política, nova categoria de produto).

### Passo 6 — Gerar as duas saídas

**Markdown** — pra leitura e aprovação rápida:

```markdown
# Pauta — [Cliente] — [Mês/Ano]

## Visão geral do mês
[1-2 parágrafos: tema central do mês, produto(s) destaque, datas-âncora]

## Publicações da semana (feed)
| Semana | Tema | Produto(s) | Abordagem | Orientação de criação | Materiais |
|---|---|---|---|---|---|

## Stories (grade diária)
| Data | Dia | Tema | Descrição |
|---|---|---|---|

## Destaques
[fixos mantidos / novidades sugeridas, se houver]

## Recomendações do ciclo anterior incorporadas
- [recomendação] → [onde entrou na grade]
```

Salvar em `clientes/<cliente>/conteudo/pautas/[ano-mes]/pauta.md`.

**Planilha (.xlsx)** — no mesmo formato de colunas de
`references/formato-planilhas.md` (abas "Publicações" e "Planejamento Stories",
mais "Destaques" se houve alteração). Salvar em
`clientes/<cliente>/conteudo/pautas/[ano-mes]/pauta.xlsx`.

Gerar as duas sempre juntas — o markdown é o que se discute e aprova em conversa, a
planilha é o formato de trabalho que o cliente já está acostumado a usar.

### Passo 7 — Confirmar antes de gerar roteiros

Não gerar os roteiros dos posts automaticamente. Apresentar a grade (markdown, com
a planilha anexa) e perguntar:

> "Essa é a pauta do mês. Quer que eu já gere os roteiros de algum item, ou revisa
> primeiro?"

---

## Regras

- Não inventar datas de sazonalidade que não estão no calendário do cliente
- Se o histórico de recomendações apontar algo que nunca virou pauta em 2+ ciclos,
  sinalizar isso explicitamente na "visão geral do mês"
- Nunca preencher retorno/métricas com valor inventado — essa coluna só é
  preenchida depois, com dado real
- A rotação de temas por dia (`temas-recorrentes.md`) é ponto de partida, não regra
  fixa — ajustar conforme o momento da marca
- Tom conforme `_contexto/preferencias.md` e, quando aplicável, o tom próprio do
  cliente
- Validação humana obrigatória antes de qualquer publicação — esta skill organiza
  a grade, não publica nada
