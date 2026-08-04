---
name: roteiro-post
description: >
  Transforma uma ideia, texto, link ou arquivo em roteiro de post para redes sociais, vídeo
  curto, thread ou newsletter, usando o contexto de um cliente já mapeado (clientes/[nome]/).
  Calibra o formato e o tom ao canal pedido. Use quando o usuário pedir "faz um roteiro",
  "transforma isso num post", "escreve um roteiro de vídeo", "cria uma thread", "faz uma
  newsletter sobre isso", ou "roteiro pro [cliente]".
---

# /roteiro-post — Roteiro de Conteúdo

## Dependências

- **Contexto do cliente:** `clientes/[nome]/AGENTS.md` (resumo) — e `clientes/[nome]/briefing.md`
  quando precisar de mais detalhe do que o resumo tem (ex: variações específicas de produto,
  histórico completo de sazonalidade)
- **Catálogo de produtos:** `clientes/<cliente>/dados/catalogo-produtos.xlsx` — fonte
  de verdade pra nome exato, capacidade, quantidade por caixa, condição do vidro e
  utilizações sugeridas. Nunca inventar essas informações; se o produto não estiver
  no catálogo, perguntar antes de escrever o roteiro.

---

## Workflow

### Passo 0 — Identificar o cliente

Checar quantas pastas existem em `clientes/`:
- **Nenhuma** — avisar: "Ainda não tem nenhum cliente mapeado. Roda /mapear-cliente primeiro."
- **Uma só** — usar ela direto, sem perguntar (não faz sentido perguntar o óbvio)
- **Mais de uma** — perguntar: "Pra qual cliente é esse roteiro?" e listar os nomes encontrados

### Passo 1 — Entender o pedido

Identificar:
1. **O conteúdo fonte:** ideia, link, texto, arquivo, transcrição ou assunto livre
2. **O formato de saída:** post Instagram, vídeo curto (Reels/TikTok), thread X/LinkedIn,
   newsletter, roteiro de YouTube

Se não estiver claro, perguntar: "Pra qual formato é esse roteiro? (post, vídeo curto, thread,
newsletter)"

Se for um link, usar WebFetch pra buscar o conteúdo.

### Passo 2 — Ler o contexto do cliente

Ler `clientes/[nome]/AGENTS.md` pra calibrar:
- Tom de voz
- Público
- Produtos/catálogo relevantes ao tema pedido
- Sazonalidade (se o pedido tiver relação com alguma data)

Se o `AGENTS.md` não tiver detalhe suficiente pra escrever bem (ex: pedido é sobre uma
variação específica de produto), consultar `briefing.md` antes de perguntar pro usuário.

**Se faltar informação que nem o AGENTS.md nem o briefing.md têm**, perguntar direto, em vez
de inventar ou generalizar:
- Se não estiver claro **o objetivo** do post (vender um produto específico, engajar, educar,
  anunciar novidade) — perguntar: "Esse roteiro é mais pra vender algo específico, engajar o
  público, ou outra coisa?"
- Se o cliente tiver algum **exemplo de post/legenda anterior que funcionou bem**, e o usuário
  mencionar ou anexar um, usar como referência de estilo real (não só a descrição de tom)

### Passo 3 — Escrever o roteiro

**Post (Instagram/LinkedIn):**
- Hook nas primeiras 2 linhas (antes do "ver mais")
- Desenvolvimento em parágrafos curtos ou lista com contexto
- CTA no final (pergunta, link, salvar)
- Sugestão de hashtags (5-10)

**Calibrando o CTA pelo objetivo:**
- Se o objetivo for **vender**, o CTA precisa deixar clara uma ação de compra/consideração —
  mesmo que o tom do cliente evite ser "vendedor", suavizar o **tom** não significa esvaziar a
  **ação**. Prefira algo como "manda DM pra garantir o seu", "disponível no site — link na
  bio", "só até [prazo/estoque]" no tom da marca, em vez de só uma pergunta de engajamento sem
  direcionamento nenhum pra compra.
- Se o objetivo for **engajar/educar**, aí sim o CTA de pergunta/comentário é o certo — não
  precisa empurrar venda.
- Se ficar em dúvida sobre até onde suavizar sem perder a força do CTA de venda, **perguntar**
  em vez de decidir sozinho: "Prefere um CTA mais direto de venda, ou mantemos mais sutil
  mesmo sendo esse o objetivo?"

**Vídeo curto (Reels/TikTok — até 60s):**
- 0-3s: hook visual + frase de abertura
- 4-20s: o problema ou a promessa
- 21-45s: a resposta ou o conteúdo principal
- 46-60s: conclusão + CTA
- Formato: linha a linha, com marcações de tempo aproximadas

**Thread (X ou LinkedIn):**
- Tweet/post 1: hook que para o scroll
- Tweets 2-8: um ponto por tweet, progressão lógica
- Tweet final: conclusão + CTA

**Newsletter:**
- Linha de assunto + pré-header (duas opções)
- Abertura pessoal (2-4 linhas)
- Desenvolvimento em seções curtas
- Encerramento com CTA

### Passo 4 — Salvar

Salvar em `clientes/[nome]/conteudo/roteiros/[ano]-[mes]/roteiro-[tema]-[data].md` — por
exemplo, `clientes/vila-aromas/conteudo/roteiros/2026-07/roteiro-difusores-2026-07-29.md`. A
subpasta usa o ano-mês em que o roteiro foi gerado (aqui não há "mês dos dados" como no
`/analisar-dados` — é sempre o mês da criação do conteúdo).

Mostrar o roteiro gerado no chat também, não só salvar — o usuário precisa revisar antes de
considerar pronto (nenhum conteúdo vai direto pra publicação sem essa revisão).

### Passo 5 — Sugerir atualizar o briefing, se for o caso

Se, durante a conversa, o usuário forneceu uma informação nova e reutilizável que não estava
em `AGENTS.md` nem `briefing.md` (ex: história/inspiração de um produto, detalhe de coleção,
contexto de campanha), sugerir no fim da resposta que isso seja registrado no `briefing.md`
do cliente — não fazer a atualização sozinho sem perguntar, só sugerir. Ex: "Essa história da
Coleção Ipê não estava no briefing.md — quer que eu registre lá pra próximas vezes?"

---

## Regras

- Tom segue `clientes/[nome]/AGENTS.md` estritamente — nunca genérico "de marca nenhuma"
- Não usar fórmulas de youtuber ("ei pessoal", "não esquece de dar like")
- O roteiro deve soar como o cliente fala, não como conteúdo genérico de IA
- Frases de transição naturais, não clichês de criador de conteúdo
- Nunca inventar informação de produto/preço/estoque que não está no contexto do cliente —
  se precisar de um dado que não existe em `AGENTS.md` nem `briefing.md`, perguntar
- Nunca inventar **alegações sociais ou comportamentais** que não vieram do contexto do
  cliente — frases como "virou ritual pra muita gente", "nossos clientes amam", "todo mundo
  comenta sobre" são afirmações de prova social, e precisam ser tratadas como dado inventado
  se não existir base real (depoimento, review, menção) no `AGENTS.md`/`briefing.md`. Se quiser
  usar esse tipo de apelo, formular como convite ("você já...?") em vez de afirmação factual
  sobre terceiros.
- Cautela com **alegações de efeito ou benefício** (ex: "ativa uma resposta no corpo", "cura",
  "elimina", "garante resultado") — preferir linguagem de experiência/percepção ("muita gente
  sente que...", "é conhecido por...") em vez de afirmação científica/médica categórica, mesmo
  que pareça senso comum. Sinalizar na seção de Observações quando uma frase desse tipo foi
  usada, pra chamar atenção na validação humana.
- Se o cliente tiver mais de um produto que se encaixa no tema pedido, perguntar qual priorizar
  em vez de escolher sozinho
- Nunca assumir **status ou disponibilidade** de um produto/campanha (se já foi lançado, está
  em pré-venda, esgotado, é edição limitada, etc.) sem confirmação. Se o pedido do usuário
  for ambíguo sobre isso (ex: "post sobre o lançamento" não deixa claro se já lançou ou vai
  lançar), perguntar antes de escrever — não decidir sozinho nem deixar isso implícito no CTA
  sem declarar a suposição na seção de Observações
- Respeitar o tom da marca (ex: "evita tom vendedor") não é motivo pra esvaziar o CTA quando o
  objetivo é venda — são duas coisas diferentes: tom é *como* se fala, CTA é *se* direciona pra
  ação. Documentar na seção de Observações como o CTA foi calibrado entre os dois.
