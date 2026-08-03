# Contexto da Operação

> Preencher/revisar manualmente (este workspace não usa o /setup automático do kit
> original — foi adaptado à mão).

**Nome:** [seu nome ou nome da operação]
**Negócio:** Sistema de conteúdo e análise de marketing, operado via Claude Code
**O que faz:** Mapeamento de negócio/marca, geração de roteiros de post, análise de
dados de vendas com memória entre ciclos, geração de arte final de posts
**Perfil:** Operação solo, com arquitetura pronta pra virar agência multi-cliente
(ver seção 9 do resumo do projeto)
**Atende clientes:** Potes & Cia (piloto, ativo)
**Equipe:** [preencher]
**Ferramentas:** Claude Code, GitHub (via `/syncar`)
**Principais entregas:** Roteiros de post, artes finais, relatórios de análise mensal

## Contexto adicional

- Arquitetura pensada desde o início pra múltiplos clientes: cada cliente é pasta
  isolada em `clientes/`, sem interferência entre eles.
- Curto prazo: ferramenta interna de agência/serviço, operada por uma pessoa.
- Longo prazo (não priorizado agora): plataforma hospedada multi-cliente — exigiria
  banco de dados e API em produção; não recomendado antes de validar o modelo atual
  com o piloto real (Potes & Cia).
