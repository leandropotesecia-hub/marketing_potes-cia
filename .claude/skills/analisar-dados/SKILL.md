---
name: analisar-dados
description: >
  Analisa um arquivo de dados (CSV, Excel, TXT, JSON) de um cliente já mapeado, gera um resumo
  executivo com insights, tendências e recomendações, e mantém um histórico de recomendações
  entre ciclos de análise — comparando o que foi sugerido antes com o que de fato mudou.
  Use quando o usuário disser "analisa esse arquivo", "o que mostram esses dados", "resume
  esses resultados", "analisa esse relatório", "análise mensal do [cliente]", ou arrastar um
  arquivo de dados.
---

# /analisar-dados — Análise de Dados com Histórico

## Dependências

- **Contexto do cliente:** `clientes/[nome]/AGENTS.md` (pra entender o que os dados representam)
- **Histórico de recomendações:** `clientes/[nome]/analises/recomendacoes.md` (se existir)

---

## Workflow

### Passo 0 — Identificar o cliente

Mesma lógica das outras skills: checar `clientes/`. Se só uma pasta, usar direto. Se mais de
uma, perguntar qual. Se nenhuma, avisar que precisa rodar `/mapear-cliente` primeiro.

### Passo 1 — Entender o contexto

Ler `clientes/[nome]/AGENTS.md` pra saber o que os dados provavelmente representam (catálogo,
canais ativos).

Perguntar, se não estiver claro pelo nome do arquivo ou conteúdo:
- "O que é esse arquivo? (vendas, anúncios, métricas de rede social, respostas de pesquisa...)"
- "Qual é a pergunta principal que você quer responder com esses dados?"

### Passo 2 — Checar histórico de recomendações

Checar se `clientes/[nome]/analises/recomendacoes.md` existe:

- **Não existe** — é a primeira análise desse cliente. Seguir direto pro Passo 3, sem essa
  etapa de comparação (seção "Acompanhamento" fica de fora do relatório).
- **Existe** — ler a tabela. Pra cada recomendação com status "Pendente" de análises
  anteriores, classificar a evidência nos dados novos antes de decidir se pergunta:

  - **Evidência forte** (a métrica-alvo da recomendação sumiu, disparou, ou mudou de forma
    inequívoca nos dados novos) — **não perguntar**. Marcar como "Seguida" ou "Não seguida"
    direto, e declarar isso no relatório e no plano de atualização do histórico ("Estou
    marcando X como Seguida, porque os dados mostram Y — avisa se não for esse o motivo real").
    Isso dá ao usuário a chance de corrigir sem forçar uma pergunta bloqueante.
  - **Evidência ambígua ou ausente** (a métrica não mudou de forma clara, ou a recomendação
    não tinha uma métrica fácil de rastrear) — aí sim perguntar, agrupando as perguntas em vez
    de uma por uma.

  Exemplos de evidência forte: um canal recomendado pra desativar cai a zero pedidos; um
  produto recomendado pra promover dobra de participação na receita. Exemplos de evidência
  ambígua: um produto recomendado pra testar continua com volume parecido (pode ou não ter
  sido testado, os dados não dizem).

### Passo 3 — Ler o arquivo de dados

Ler o arquivo fornecido. Se for Excel (.xlsx), ler com as ferramentas disponíveis pra extrair
o conteúdo das células.

### Passo 4 — Análise

Identificar e reportar:

**Acompanhamento do ciclo anterior** (só se houver histórico — Passo 2):
- O que foi recomendado e foi seguido — e o que aconteceu com a métrica relacionada
- O que foi recomendado e não foi seguido (sem julgar o motivo, só registrar)

**O que está bom:**
- Métricas acima da média ou em crescimento
- Padrões positivos nos dados
- Top performers (produtos, campanhas, períodos, etc)

**O que preocupa:**
- Quedas, anomalias ou tendências negativas
- O que está abaixo do esperado
- Gargalos ou desperdícios visíveis

**Comparações:**
- Período atual vs período anterior (se houver)
- Top vs bottom performers
- Distribuição entre categorias

**Insights não óbvios:**
- Correlações interessantes
- Padrões que não aparecem na leitura superficial

### Passo 5 — Output

Gerar um resumo executivo em prosa (não só bullet points):

```markdown
# Análise — [Nome do Arquivo/Relatório]
*[Data da análise] — Cliente: [nome]*

## Acompanhamento do ciclo anterior
[só incluir se houver histórico — o que foi seguido, o que não foi, e o efeito observado]

## O que esses dados mostram
[2-3 parágrafos com o panorama geral]

## O que está funcionando
[lista com contexto]

## O que merece atenção
[lista com contexto]

## 3 recomendações pra esse ciclo
1. [ação concreta]
2. [ação concreta]
3. [ação concreta]

## Números-chave
| Métrica | Valor | Contexto |
|---------|-------|---------|
| ... | ... | ... |
```

Salvar em `clientes/[nome]/analises/[ano]-[mes]/analise-[tema]-[data].md` — por exemplo,
`clientes/vila-aromas/analises/2026-07/analise-vendas-julho-2026.md`. A subpasta usa o
ano-mês a que os dados analisados se referem (não a data em que a análise foi rodada, caso
sejam diferentes — ex: analisando dados de julho em agosto, a subpasta é `2026-07`).

**Sempre perguntar** se quer exportar o resumo em HTML pra compartilhar ou apresentar — essa
pergunta não pode ser esquecida nem em ciclos que têm a etapa extra de comparação com o
histórico (Passo 2). Se o usuário disser sim, o HTML deve ter: cards com os números-chave no
topo, um parágrafo de resumo geral, gráfico de barra simples pra categoria e canal (ou a
dimensão mais relevante dos dados), listas de "o que está funcionando" / "o que merece
atenção", e a lista de recomendações — seguindo o mesmo estilo visual já usado nas análises
anteriores desse cliente, se houver uma pra copiar o padrão. Salvar na mesma subpasta do `.md`
correspondente.

Se o usuário disser sim e o ambiente permitir gerar um link de preview do artifact
(`claude.ai/code/artifact/...`), oferecer esse link também — é a forma mais fácil de
compartilhar sem precisar abrir o arquivo local.

### Passo 6 — Atualizar o histórico de recomendações

Atualizar (ou criar, se for a primeira vez) `clientes/[nome]/analises/recomendacoes.md`:

```markdown
# Histórico de recomendações — [Nome do Cliente]

| Data | Recomendação | Status | Resultado observado |
|------|--------------|--------|---------------------|
| [data] | [texto] | Pendente | — |
```
(Status possíveis depois de atualizado: Pendente, Seguida, Não seguida, Ainda pendente, Sem
evidência suficiente — ver critério de cada um abaixo)

- As 3 recomendações desse ciclo entram como linhas novas, status "Pendente"
- As recomendações de ciclos anteriores mudam de status conforme o que foi confirmado
  (Passo 2) ou inferido dos dados — usar um destes quatro status, nunca só "sim/não":
  - **Seguida** — foi feita, com resultado observável
  - **Não seguida** — decisão explícita de não fazer (ex: usuário confirmou que optou por não
    seguir aquele caminho)
  - **Ainda pendente** — não foi feita, mas segue válida; se o mesmo tema virar recomendação
    de novo nesse ciclo, linkar as duas (ex: "ver também recomendação de [data]")
  - **Sem evidência suficiente** — não deu pra confirmar nem pelos dados nem pela resposta do
    usuário; mencionar no relatório que ficou em aberto
  Não usar "Não seguida" como padrão genérico pra qualquer coisa que não aconteceu — só quando
  há confirmação de que foi uma escolha deliberada de não fazer.

Mostrar o plano antes de escrever ("vou atualizar o histórico de recomendações com X, Y, Z —
bora?") e só então salvar.

---

## Regras

- Análise em prosa, não só listas — o usuário deve poder ler e entender sem abrir o arquivo
  original
- O `.md` é sempre gerado. O HTML é opcional e só é criado se o usuário confirmar quando
  perguntado — mas a pergunta em si nunca pode ser esquecida, mesmo em ciclos com a etapa
  extra de comparação com o histórico (Passo 2)
- Nunca inventar dados que não estão no arquivo
- Nunca inventar se uma recomendação foi seguida ou não — perguntar ou usar evidência clara
  dos dados, nunca supor
- Se os dados estiverem incompletos ou com problemas, mencionar antes de analisar
- Tom conforme `clientes/[nome]/AGENTS.md`
- Recomendações precisam ser específicas e acionáveis (não "melhorar o engajamento", e sim
  "postar mais conteúdo de [categoria X], que teve [métrica] acima da média")
