# Formato das planilhas — referência de colunas

> Baseado em `Planejamento_Publicações.xlsx` e `Planejamento_Stories_e_Destaques.xlsx`
> (histórico da agência anterior, 2022). A skill gera novas planilhas nesse mesmo
> formato de colunas, com conteúdo atual — não edita os arquivos antigos.

## Aba "Publicações" (post semanal principal — feed)

Colunas, nessa ordem:

| Coluna | Conteúdo |
|---|---|
| Mês | Só na primeira linha do mês (ex: "MAIO") |
| Semana | "Sem 1", "Sem 2"... |
| Tema | Nome curto do post |
| Produto(s) | Produto(s) específico(s) envolvidos, se houver |
| Utilidade / Abordagem | Contexto de uso ou público-alvo do post |
| Orientação para criação / legenda | Direção pro roteiro/legenda (isso é o insumo direto pro `/roteiro-post`) |
| Materiais Adicionais | Formatos extras (Story, Banner, Google, etc.) |
| Orientações Gerais | Observações gerais de campanha |
| OBS. | Observações livres |

## Aba "Planejamento Stories" (grade diária)

Colunas, nessa ordem:

| Coluna | Conteúdo |
|---|---|
| Mês / Semana | Mês na primeira linha, "SEM 1" etc. por bloco |
| Dia | Dom/Seg/Ter/Qua/Qui/Sex/Sáb |
| Data | Dia do mês (número) |
| Tema | Um dos temas da rotação (ver `temas-recorrentes.md`) |
| Descrição | O que postar especificamente naquele dia |
| Retorno | **Deixar em branco na geração** — é preenchido depois de postar, com base em métricas reais. Não inventar número aqui. |

## Aba "Destaques"

Colunas: Tema, Descrição, Observações. Só atualizar se houver destaque novo a
sugerir — a maioria é fixa (ver lista em `temas-recorrentes.md`).

## Regra geral de geração

- Gerar as duas abas (Publicações e Stories) sempre juntas, referentes ao mesmo mês.
- Se o cliente tiver produto(s) em destaque do mês (definido no Passo 3 do
  `SKILL.md`), esse produto deve aparecer tanto na aba Publicações quanto reforçado
  na rotação de Stories da(s) primeira(s) semana(s).
- Nunca preencher a coluna de retorno/métricas com valor inventado.
