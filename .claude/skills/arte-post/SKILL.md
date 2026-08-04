---
name: arte-post
description: >
  Cria a imagem/arte final pra acompanhar um roteiro de post já gerado pelo /roteiro-post.
  Usa foto real do produto quando disponível; quando não tiver, cria um card promocional com
  as cores e tipografia da marca (nunca fabrica uma "foto" de produto real). Renderiza via
  Playwright. Use quando o usuário disser "cria a imagem do post", "faz a arte desse roteiro",
  "gera a foto do produto pro post", "cria o visual do post", ou "imagem pra postagem".
---

# /arte-post — Imagem pra acompanhar o post

## Dependências

- **Catálogo de produtos:** `clientes/<cliente>/dados/catalogo-produtos.xlsx` — conferir
  nome exato e capacidade do produto antes de gerar a arte. Continua valendo a regra de
  nunca substituir a foto do produto sem confirmação do usuário — o catálogo informa o
  texto, não substitui a foto real.

## Passo 0 — Identificar cliente e roteiro

Mesma lógica de identificação de cliente das outras skills. Depois, perguntar (se não estiver
claro) qual roteiro essa imagem é pra acompanhar — listar os roteiros recentes em
`clientes/[nome]/conteudo/roteiros/` se precisar ajudar o usuário a lembrar.

Ler o roteiro escolhido pra saber: produto, mensagem principal, e se tem preço/promoção pra
destacar.

## Passo 1 — Checar identidade visual

Ler `clientes/[nome]/marca/design-guide.md`.

- **Se não existir ou estiver vazio**: avisar — "Esse cliente ainda não tem guia de marca.
  Rodo /mapear-marca primeiro, ou você prefere que eu use um padrão neutro só pra essa arte?"
- **Se existir**: usar as cores, tipografia e estilo definidos lá.

## Passo 2 — Foto real ou card promocional

Perguntar:
> "Você tem uma foto real do produto (a Garrafa Âmbar Caçula, nesse caso)? Pode anexar aqui.
> Se não tiver, eu crio um card promocional com o nome do produto e a chamada do post, usando
> as cores da marca — sem tentar desenhar uma 'foto' do produto, pra não arriscar sair
> diferente do produto de verdade."

- **Se o usuário anexar foto real**: usar essa foto como base, **respeitando o padrão de
  composição registrado em `design-guide.md`** (seção "Composição de fotos"):

  - **Hierarquia: a foto domina o quadro, o texto é discreto.** Olhando um post real como
    referência: a foto ocupa a maior parte da imagem (produto grande, em primeiro plano); o
    texto (nome, preço, badges) fica compacto, geralmente num canto ou faixa lateral/inferior
    — nunca um título gigante centralizado empurrando a foto pra um espaço pequeno no meio.
    Se a composição atual estiver saindo "texto grande em cima, foto pequena no meio", isso
    está invertido e precisa ser refeito.
  - Se o padrão for **cenário real** (cozinha, balcão, mesa) e a foto disponível não tiver
    esse cenário (ex: recorte de catálogo com fundo branco/transparente): perguntar se o
    usuário quer (a) usar como está, sobre fundo com cor da marca, ou (b) gerar um fundo
    contextual via IA pra compor atrás do produto (ver "Fundo gerado por IA" abaixo)
  - Se o padrão for **fundo de estúdio/abstrato**, ou não houver padrão definido: aí sim vale
    isolar o produto sobre um fundo com as cores da marca — mas mantendo o produto grande
    (ver hierarquia acima), não pequeno e centralizado
  - Preço: **mostrar por padrão** se o roteiro tiver essa informação, a menos que o usuário
    tenha decidido explicitamente não mostrar (confirmar isso antes de omitir, não assumir).
    O badge de preço deve ser **compacto e posicionado num canto** (como observado em post
    real), não uma pílula grande centralizada
  - CTA/canais de venda (Mercado Livre, Shopee, site): **só incluir na arte se o
    `design-guide.md` indicar que os posts reais costumam ter isso na imagem** — se a
    informação só costuma aparecer na legenda/bio, não replicar isso dentro da arte
  - **Nunca adicionar elementos decorativos que não vieram de um padrão observado** — tags de
    ocasião ("DIA DOS PAIS" em badge no topo), efeitos de glow/brilho artificial, texturas ou
    qualquer enfeite visual só existem na arte se `design-guide.md` registrar que posts reais
    realmente têm esse elemento. Na dúvida, omitir — menos é mais seguro que inventar
- **Se o usuário mandar um link** (da página do produto, ou link direto da imagem): tentar
  obter a imagem exata daquela página/link — nunca substituir por uma imagem "parecida" achada
  por outro meio. Depois de obter (ou tentar obter), **mostrar a imagem encontrada e perguntar
  explicitamente se é a foto certa** antes de seguir. Se não conseguir obter a imagem exata,
  dizer isso claramente ("não consegui baixar a imagem exata dessa página — pode anexar o
  arquivo direto, ou me passar o link direto da imagem?") em vez de prosseguir com qualquer
  substituto.
- **Se não tiver foto**: seguir pro card promocional (Passo 3).

### Fundo gerado por IA (opcional, quando não há foto em cenário real)

Se o padrão da marca pede cenário real mas a única foto disponível for de catálogo (fundo
branco/isolado), oferecer gerar um fundo contextual via Pollinations.ai (gratuito, sem
cadastro, sem risco de direito autoral por ser gerado na hora):

```bash
curl -L "https://image.pollinations.ai/prompt/[descrição%20do%20cenário%2C%20sem%20texto%2C%20sem%20logo]?width=1080&height=1350&nologo=true" -o fundo-gerado.jpg
```

O prompt deve descrever só o cenário (ex: "wooden table, blurred bar shelf background, warm
lighting"), nunca o produto em si (o produto continua sendo a foto real, só o fundo é gerado).

**Obrigatório**: registrar nas Observações do arquivo final que o fundo é gerado por IA, não
uma foto real do espaço do cliente — ex: "Fundo gerado por IA pra compor com a foto real do
produto; não representa o espaço físico real da Potes & Cia. Se decidirem fazer conteúdo de
'bastidor real' no futuro, precisa ser fotografado de verdade."

## Passo 3 — Card promocional (quando não há foto)

Criar um HTML de card único (1080x1350, formato feed Instagram) usando:
- Fundo e cor de destaque do `design-guide.md`
- Nome do produto ou tema em destaque (tipografia bold/impacto, conforme o guia) — sem ocupar
  a maior parte do quadro; deixar espaço visual generoso, não lotar a peça de texto
- Uma chamada visual curta e de impacto — **não copiar literalmente a legenda do roteiro**;
  a legenda foi escrita pra ser lida como texto corrido, a arte precisa de algo mais curto e
  visualmente forte (ex: se a legenda fala em "garanta o lote da temporada", a arte pode usar
  só "GARANTA O SEU" ou algo do mesmo espírito, mas adaptado pro formato de poucas palavras)
- Preço: mostrar por padrão se o roteiro tiver essa informação, seguindo a mesma regra do
  Passo 1 — badge **compacto, num canto**, não uma pílula grande centralizada
- Canais de venda: só incluir se `design-guide.md` indicar que aparece nos posts reais —
  nunca adicionar por padrão só porque está mencionado no roteiro
- Logo, se o cliente tiver um cadastrado no design-guide
- **Nunca adicionar tags de ocasião, glow/brilho artificial ou qualquer elemento decorativo
  que não venha de um padrão observado em `design-guide.md`** — mesma regra do Passo 1

Não inventar elementos visuais que sugiram ser "foto do produto" (sombra realista, textura de
vidro, reflexo) — o card deve parecer claramente uma peça gráfica/promocional, não uma
fotografia.

## Passo 4 — Renderizar

Checar se Playwright está instalado:
```bash
npx playwright screenshot --help 2>/dev/null && echo "OK" || echo "INSTALAR"
```
Se precisar instalar, avisar o usuário que vai demorar ~30s na primeira vez:
```bash
npx playwright install chromium
```

Renderizar o HTML em PNG:
```bash
npx playwright screenshot --viewport-size=1080,1350 --full-page "file:///caminho/absoluto/arte.html" "arte.png"
```

Mostrar o resultado (a imagem gerada) pro usuário antes de considerar pronto.

## Passo 5 — Salvar

Salvar em `clientes/[nome]/conteudo/postagens/[ano]-[mes]/`:
- `arte-[tema]-[data].html` (fonte editável)
- `arte-[tema]-[data].png` (imagem final)

Mostrar o plano antes de salvar, mesmo padrão de sempre.

---

## Regras

- **Nunca fabricar uma "foto" de produto real** — se não houver foto de verdade, o resultado
  é sempre um card/peça gráfica claramente promocional, nunca uma tentativa de simular
  fotografia do produto
- **Nunca substituir a foto real pela mais parecida disponível.** Se o usuário anexou ou
  apontou uma foto específica (arquivo, print, ou link direto da página do produto), a imagem
  usada precisa ser **exatamente aquela** — nunca uma imagem "similar" obtida por busca,
  banco de imagens, ou qualquer fallback. Se não for tecnicamente possível obter a imagem
  exata apontada pelo usuário (link quebrado, formato não suportado, etc.), **parar e avisar
  explicitamente** — nunca prosseguir usando uma imagem parecida sem dizer que trocou.
- **Antes de montar a arte, mostrar a imagem que será usada e pedir confirmação explícita**
  de que é o produto certo (ex: "essa é a foto que vou usar — confere com o produto real?").
  Isso vale mesmo quando a imagem veio de download automático a partir de um link — nunca
  pular direto pra renderização sem esse checkpoint visual.
- Se o usuário fornecer foto real, ela nunca é alterada digitalmente além de overlay de texto
  (nada de "melhorar" ou redesenhar a foto)
- Cores e tipografia seguem `design-guide.md` estritamente — nunca escolher paleta própria se
  o cliente já tiver uma definida
- Respeitar a seção "O que NUNCA fazer" do `design-guide.md`, se preenchida
- Sempre mostrar a imagem renderizada antes de considerar a tarefa concluída — nenhuma arte
  vai "direto pra pasta" sem o usuário ver o resultado
- **A foto do produto sempre domina visualmente o quadro; texto e badges são discretos e
  compactos**, nunca um título grande empurrando a foto pra um espaço pequeno — comparar
  mentalmente com um post real antes de finalizar
- **Nunca inventar elemento decorativo** (tag de ocasião, glow, textura) que não esteja
  registrado como padrão real em `design-guide.md`
- Se usar fundo gerado por IA, **sempre registrar isso nas Observações**, deixando claro que
  não é o espaço físico real do cliente
- Esta skill só cria a imagem — nunca publica. Publicação é responsabilidade de uma skill
  separada (ainda não construída)
