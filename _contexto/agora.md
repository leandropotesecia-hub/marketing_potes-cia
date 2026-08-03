# Agora — contexto vivo

> Este é o contexto que muda toda semana. Mantenha curto: o que passou de ~30 dias
> sai daqui (vai pro histórico ou some).

## Onde paramos

A skill `/pauta-mensal` (7ª skill do workspace) foi construída, testada e validada
com sucesso: gerou a pauta de Agosto/2026 da Potes & Cia (`pauta.md` + `pauta.xlsx`
em `clientes/potes-e-cia/conteudo/pautas/2026-08/`), respeitando a ordem de
publicação já decidida (Garrafa Âmbar Caçula antes do post de retomada) e
sinalizando corretamente o que não pôde confirmar (sem histórico de
`/analisar-dados` ainda; destaques do perfil podem estar desatualizados após ~1 ano
parado). Próximo passo: revisar a pauta gerada e desdobrar os itens em roteiros.

## Decisões recentes

- Estrutura de cliente segue o padrão: artefato com recorte de tempo → subpasta
  `[ano-mes]/`; artefato de estado atual → sem data no caminho
- Regra travada: nunca trocar imagem de produto sem confirmação (causou erro real
  na primeira arte gerada)
- `/pauta-mensal` gera sempre markdown + xlsx juntos, usando a rotação de temas por
  dia da semana extraída do histórico real da agência anterior (2022) como base
- `/pauta-mensal` nunca preenche métricas/retorno com valor inventado — fica em
  branco até ter dado real pós-publicação

## Pendências

- Revisar a pauta.md/pauta.xlsx de Agosto/2026 e aprovar antes de gerar roteiros
- Levantar concorrência da Potes & Cia
- Verificar manual de marca oficial da agência anterior
- Conseguir fotos de produto em cenário real (hoje só tem fundo branco de catálogo)
- Rodar `/analisar-dados` pela primeira vez pra começar o histórico de
  `recomendacoes.md` (hoje ainda não existe)

## Quente agora

Revisão da pauta de Agosto/2026 da Potes & Cia e decisão de quais itens viram
roteiro primeiro (Sem 1 já tem conteúdo pronto; Sem 2 depende do Dia dos Pais,
09/08).
