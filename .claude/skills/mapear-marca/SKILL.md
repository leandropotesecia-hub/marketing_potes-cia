---
name: mapear-marca
description: >
  Captura a identidade visual (cores, tipografia, estilo, logo) de um cliente já mapeado e
  gera clientes/[nome]/marca/design-guide.md. Aceita link do site, imagens de referência,
  descrição em texto, ou nenhum material ainda (nesse caso mostra um exemplo pra inspirar).
  Use quando o usuário disser "mapear a marca do [cliente]", "definir identidade visual",
  "guia de marca do cliente", "preciso da identidade visual da [cliente]", "configurar a
  marca de [cliente]", ou "criar o design guide do [cliente]".
---

# /mapear-marca — Identidade Visual do Cliente

## Passo 0 — Identificar o cliente

Mesma lógica das outras skills: checar `clientes/`. Se só uma pasta, usar direto. Se mais de
uma, perguntar qual. Se nenhuma, avisar que precisa rodar `/mapear-cliente` primeiro (a marca
depende de o cliente já existir).

Checar se `clientes/[nome]/marca/design-guide.md` já existe — se sim, perguntar se quer
refazer do zero ou só ajustar algo pontual.

## Passo 1 — Perguntar como o material vai chegar

"Como você quer me passar a identidade visual? Você pode:
1. Mandar o link do site/Instagram do cliente (eu extraio cores e estilo de lá)
2. Anexar uma imagem de referência (arte, logo, print)
3. Descrever em texto (cores que já usa, estilo que imagina)
4. Ainda não tem nada definido — nesse caso te mostro um exemplo pra você se inspirar"

### Caminho 1 — Link
Usar WebFetch pra ler o site/perfil. Extrair: paleta de cores predominante, estilo de
tipografia (serifada/sem serifa, arredondada/reta), tom visual geral (clean, colorido,
minimalista, maximalista). Mostrar o que foi detectado antes de gravar:
> "Vi no site: fundo [cor], destaque em [cor], tipografia [estilo], sensação geral [adjetivo].
> Bate com a marca? Quer ajustar algo?"

### Caminho 2 — Imagem
Analisar a imagem anexada visualmente. Mesma lógica de mostrar o que foi detectado antes de
gravar, igual ao Caminho 1.

### Caminho 3 — Texto
Perguntar, se a descrição vier vaga, por pelo menos: cor principal, cor de destaque/CTA, e um
adjetivo de estilo geral (ex: "moderno e minimalista" vs "quente e artesanal").

### Caminho 4 — Ainda não tem nada definido
Mostrar um exemplo preenchido pra servir de referência (não pra copiar literalmente, pra
mostrar o nível de detalhe esperado):

> "Sem problema, aqui vai um exemplo de como fica um guia completo, pra você se inspirar:
>
> *Cores: fundo #FAF7F2, destaque #C96442, texto #1C1917 — tons terrosos e quentes*
> *Tipografia: títulos em serifa leve, corpo em sans-serif*
> *Estilo: quente, humano, editorial — parece um diário de marca pessoal*
> *O que nunca fazer: fundo branco puro, bordas retas sem arredondamento*
>
> Baseado no que você já sabe do [nome do cliente] (tom de voz, público), você tem uma
> direção de cor ou estilo em mente? Ou prefere deixar em branco por agora e preencher depois?"

Se o usuário preferir deixar em branco, gerar o arquivo com a estrutura vazia e um comentário
"ainda não definido — rode /mapear-marca de novo quando tiver referência".

## Passo 2 — Gerar o arquivo

```markdown
# Guia de Design — [Nome do Cliente]

## Cores
- **Fundo principal:** [cor ou "não definido"]
- **Cor de destaque / CTA:** [cor ou "não definido"]
- **Texto principal:** [cor ou "não definido"]
- **Cor proibida:** [se houver]

## Tipografia
- **Títulos e destaques:** [fonte/estilo ou "não definido"]
- **Corpo:** [fonte/estilo ou "não definido"]

## Estilo geral
[1-2 frases descrevendo a sensação visual — ex: "quente e artesanal" vs "clean e moderno"]

## O que NUNCA fazer
[lista de restrições visuais, se houver]

## Logo
- **Arquivo:** [caminho, se o usuário tiver enviado]
- **Onde usar:** [contexto de uso, se souber]
```

Salvar em `clientes/[nome]/marca/design-guide.md`.

Mostrar o plano antes de criar ("vou salvar o guia de marca do [cliente] assim — bora?") e só
então gravar.

## Passo 3 — Avisar as skills de conteúdo

Informar ao usuário: "Esse design guide fica disponível pra skills futuras que gerem conteúdo
visual (carrossel, slide, etc). O `/roteiro-post` de hoje não usa isso, já que só gera texto."

---

## Regras

- Nunca inventar cor, fonte ou estilo — se não tiver material nenhum, usar o Caminho 4
  (exemplo + pergunta), nunca supor uma paleta "genérica bonita"
- Sempre mostrar o que foi detectado (de link ou imagem) antes de gravar, esperando confirmação
- Se o cliente não tiver nada definido ainda, tudo bem gerar o arquivo incompleto — melhor
  registrar o que existe do que forçar decisão que o usuário não tem ainda
