---
name: mapear-cliente
description: >
  Entrevista o usuário sobre o negócio de um cliente novo (produtos/catálogo, público-alvo,
  canais ativos, tom de voz, sazonalidade, concorrência) e gera dois arquivos em
  clientes/[nome]/: um AGENTS.md resumido (contexto rápido, lido em toda sessão de trabalho
  com esse cliente) e um briefing.md completo com o detalhe bruto da entrevista, consultado
  pelas skills de conteúdo (roteiro-post, carrossel, analisar-dados) quando precisarem de
  informação específica do catálogo ou do público. Use quando o usuário disser "mapear esse
  negócio", "preciso mapear um cliente novo", "novo cliente entrando", "fechei um cliente
  novo", "entender o negócio da [cliente]", "levantar informações desse cliente", ou
  "configurar um cliente novo no sistema".
---

# /mapear-cliente — Mapeamento de negócio de cliente novo

## Verificação inicial

Verificar se `clientes/[nome]/briefing.md` já existe. Se sim, perguntar se o usuário quer
refazer a entrevista inteira ou só atualizar uma categoria específica.

## Onboarding — a entrevista

Fazer as perguntas em sequência, **uma por vez**, esperando a resposta antes de seguir pra
próxima. Se a resposta vier vaga, fazer uma pergunta de acompanhamento antes de continuar.

Em qualquer pergunta, o usuário pode responder de três formas — todas válidas:
- **Texto corrido**, respondendo direto
- **Anexando um arquivo ou planilha** (ex: catálogo de produtos, lista de datas comemorativas)
  — ler o conteúdo e extrair a informação relevante pra aquela categoria
- **"Não sei" / "não tenho essa informação"** — aceitar, marcar como pendente no arquivo
  gerado, e seguir pra próxima pergunta sem insistir

### Pergunta 0 — Nome do cliente
"Qual é o nome do cliente ou negócio que vamos mapear?"

Usar essa resposta pra nomear a pasta `clientes/[nome]/` (versão em minúsculas, com hífen no
lugar de espaço — ex: "Potes & Cia" vira `potes-e-cia`).

### Pergunta 1 — Catálogo
"Me fala sobre o catálogo de produtos: quais são as categorias principais, e tem algum tipo
de variação que muda por produto (tipo tamanho, tampa, cor)?"

*(Exemplo: "vendemos potes e garrafas de vidro, com tampas compatíveis variando por tipo —
cliente pode usar pra mel, azeite, velas, conservas...")*

### Pergunta 2 — Público-alvo
"Quem são seus clientes? Pensa em quem compra de verdade: são pessoas físicas ou outros
negócios, pra que eles usam o produto, e se tem algum perfil que se repete."

*(Exemplo: "principalmente pequenos produtores artesanais — de mel, geleia, cachaça, velas —
que compram pote/garrafa pra embalar o próprio produto; também tem gente comprando pra
presente ou decoração")*

### Pergunta 3 — Canais ativos
"Em quais redes ou canais vocês já publicam ou vendem hoje, e qual desses é o mais importante
pra vocês agora?"

*(Exemplo: "Instagram é o principal, também vendemos pelo WhatsApp e temos Mercado Livre, mas
não damos atenção nenhuma pra ele")*

### Pergunta 4 — Tom de voz
"Como vocês falam com o cliente hoje — mais formal, mais próximo? Tem alguma expressão que é
a cara da marca, e algo que definitivamente não combina com vocês?"

*(Exemplo: "informal e simpático, sem forçar gíria; evitamos parecer 'vendedor chato'")*

### Pergunta 5 — Sazonalidade
"Tem época do ano ou data comemorativa que sempre puxa mais venda de algum produto
específico?"

*(Exemplo: "festa junina puxa garrafa pra licor/cachaça, dia dos namorados puxa pote pra
presente")*

### Pergunta 6 — Concorrência
"Quem você considera concorrente direto, e tem algo que eles fazem que você admira ou
definitivamente não quer copiar?"

*(Exemplo: "tem duas lojas de embalagem na cidade — uma foca em preço baixo, a gente quer se
diferenciar por variedade e atendimento")*

---

## O que gerar

Só depois que todas as perguntas forem respondidas — não gerar arquivo a um durante a
entrevista.

### 1. Mostrar o plano antes de criar

> "Vou criar `clientes/[nome]/` com dois arquivos: `AGENTS.md` (resumo, lido sempre que
> trabalharmos com esse cliente) e `briefing.md` (a entrevista completa). Bora?"

Só criar depois da confirmação.

### 2. Criar `clientes/[nome]/briefing.md`

```markdown
# Briefing completo — [Nome do Cliente]

## Catálogo
[resposta completa da Pergunta 1]

## Público-alvo
[resposta completa da Pergunta 2]

## Canais ativos
[resposta completa da Pergunta 3]

## Tom de voz
[resposta completa da Pergunta 4]

## Sazonalidade
[resposta completa da Pergunta 5]

## Concorrência
[resposta completa da Pergunta 6]

---
*Entrevista realizada em [data]. Pra atualizar, rode /mapear-cliente de novo.*
```

### 3. Criar `clientes/[nome]/AGENTS.md`

```markdown
# [Nome do Cliente] — Contexto

## O que é
[1-2 frases: o que vende, pra quem, resumindo catálogo + público]

## Produtos
[resumo curto das categorias principais]

## Público
[resumo curto de quem compra e pra quê]

## Canais ativos
[lista dos canais, marcando o principal]

## Tom de voz
[resumo curto do estilo de comunicação]

## Sazonalidade
[principais datas/épocas que puxam venda]

## Concorrência
[resumo breve — 1-2 linhas]

---
> Detalhe completo da entrevista em `briefing.md`. As skills de conteúdo (roteiro-post,
> carrossel, analisar-dados) devem consultar este arquivo primeiro; só abrir o briefing.md
> quando precisarem de mais detalhe do que está aqui.
```

Criar também `clientes/[nome]/CLAUDE.md` com uma linha: `@AGENTS.md` (padrão do kit).

### 4. Verificar/atualizar o AGENTS.md principal

**Esta etapa roda sempre**, independente de qual caminho a skill seguiu (entrevista nova,
refazer, ou completar pendências) — não é exclusiva do fluxo de cliente novo.

Checar se `AGENTS.md` existe na raiz do projeto:

- **Se existir**: conferir se a pasta `clientes/[nome]/` já está referenciada na seção de
  estrutura de pastas. Se não estiver, adicionar. Se já estiver, não duplicar.
- **Se não existir, ou não tiver seção de estrutura de pastas**: não falhar silenciosamente —
  avisar o usuário:

  > "Criei/atualizei a pasta do cliente. Não encontrei um AGENTS.md principal na raiz do
  > projeto pra referenciar essa pasta — se quiser, roda /setup primeiro, ou adiciona a
  > referência manualmente depois."

### 5. Confirmar

```
Cliente mapeado!

Pasta: clientes/[nome]/
AGENTS.md — resumo pronto
briefing.md — entrevista completa salva

Pra trabalhar com esse cliente, é só falar — o agente já lê o contexto da pasta.
```

## Regras

- Uma pergunta por vez. Nunca listar as 6 de uma vez.
- Toda pergunta vem com um exemplo entre parênteses mostrando o *tipo* de resposta esperada —
  nunca sugerindo a resposta certa.
- Nunca perguntar métrica que o cliente provavelmente não rastreia (ex: CAC, LTV, margem).
  Se precisar de dado desse tipo depois, perguntar separadamente com uma opção de "não sei".
- Evitar perguntas redundantes entre categorias (ex: não perguntar "público-alvo" e depois
  "demografia do cliente ideal" como se fossem coisas diferentes).
- Não assumir resposta futura — perguntar "há planos de X" em vez de "quanto vai crescer X".
- Gerar os dois arquivos só no final, depois de todas as respostas.
- Sempre mostrar o plano (pasta + arquivos) antes de criar, esperar confirmação.
- Nunca sobrescrever um `briefing.md` já existente sem perguntar antes.
- A checagem do `AGENTS.md` principal (passo 4) roda **sempre**, mesmo quando o cliente já
  existia e só foram completadas categorias pendentes — não é exclusiva de cliente novo.
- Tom direto, conversa natural, sem listar tudo de uma vez.
