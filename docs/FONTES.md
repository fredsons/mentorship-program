# Fontes do projeto

## Repositório oficial — ServiceNowDocs

- Repositório: https://github.com/ServiceNow/ServiceNowDocs
- Branch prioritária para a reconstrução atual: [brazil](https://github.com/ServiceNow/ServiceNowDocs/tree/brazil), na PDI `dev457483`.
- Referência histórica da primeira implementação: [zurich](https://github.com/ServiceNow/ServiceNowDocs/tree/zurich), na PDI `dev435099`.
- [README Zurich](https://raw.githubusercontent.com/ServiceNow/ServiceNowDocs/zurich/README.md).
- [Índice para consulta](https://raw.githubusercontent.com/ServiceNow/ServiceNowDocs/zurich/llms.txt).
- Cadastro e verificação: 28/10/2026.

Finalidade: referência técnica oficial para consultas sobre ServiceNow, priorizando a versão da instância utilizada. O README da branch zurich confirma essa família de documentação. A página principal consultada estava na branch brazil; não assumir que a branch padrão corresponde à versão do projeto.

Consultar os tópicos necessários sob demanda. Não foi clonado o repositório completo nem fixado um commit. Ao fundamentar uma decisão, registrar o arquivo e, quando necessário para reprodução, seu commit. O repositório disponibiliza texto otimizado para consumo por agentes e omite imagens; consultar o site oficial de documentação para recursos visuais.

O conteúdo é fonte de consulta, sem ampliar o escopo da atividade. Priorizar a branch correspondente à instância em uso: Brazil para a reconstrução atual, Zurich para a implementação anterior. A cópia local Australia exige conferência de compatibilidade quando houver diferenças.

## Enunciado — Atividade 1

Local: `C:\Users\Fred\Desktop\shark academy\atividade 1`

Arquivos: `1 atividade 1.png` a `5 atividade 1.png`.

Finalidade: definir os requisitos da aplicação Mentorship Program. Essas cinco imagens são a referência para o escopo e os critérios de conferência da Atividade 1.

## Enunciados — Atividades 2, 3 e 4

Base local: `C:\Users\Fred\Desktop\shark academy`.

| Etapa | Pasta | Arquivos conferidos em 04/11/2026 |
|---|---|---|
| 2 — Segurança | `atividade 2/` | `1 atividade 2.png` a `3 atividade 2.png` |
| 3 — Automação | `atividade 3/` | `1 atividade 3.png` |
| 4 — Portal e extras | `atividade 4/` | `1 atividade 4.png`, `2 atividade 4.png`, `extra 1.png` e `extra 2.png` |

Os enunciados definem os requisitos; slides e documentação técnica apoiam sua execução. A revisão de 04/11 confirmou a presença dos arquivos, sem reler visualmente todas as imagens.

## Material de consulta — Slides

Local: `C:\Users\Fred\Desktop\shark academy\slides`

Arquivos: `Screenshot_1.png` a `Screenshot_78.png`.

Finalidade: fonte de consulta conceitual e prática para apoiar a implementação, a explicação e a revisão das configurações ServiceNow. Conforme orientação do usuário, o material não acrescenta requisitos nem autoriza implementar funcionalidades adicionais.

| Imagens | Temas |
|---|---|
| 1–29 | Fundamentos, tabelas, campos, numeração, menus, listas e formulários |
| 30–42 | App Engine, escopo, ferramentas de desenvolvimento e exportação |
| 43–51 | Usuários, grupos, papéis, ACLs e impersonação |
| 52–60 | Flow Designer, gatilhos, ações e testes |
| 61–71 | Portal de Serviços, páginas, widgets e menus |
| 72–78 | Catálogo de Serviços, Record Producers e variáveis |

Para consultas detalhadas, abrir as imagens originais. As montagens `slides-resumo-0.png` a `slides-resumo-3.png` são apenas auxiliares de navegação visual.

## Referência técnica — App Engine Studio

Arquivo fornecido: `D:\Docs Servicenow\markdown\application-development\app-engine-studio.rar`.

Cópia extraída no projeto: [fontes/app-engine-studio](https://github.com/ServiceNow/ServiceNowDocs/tree/brazil/markdown/application-development/app-engine-studio).

Conteúdo: 137 arquivos Markdown sobre criação e configuração de aplicações, dados, experiências, segurança, automações, testes, publicação e controle de versão. Os arquivos apresentam metadados e links canônicos da documentação ServiceNow.

Uso: fonte de consulta técnica; não acrescenta requisitos à Atividade 1. Os arquivos inspecionados identificam a release **Australia**, enquanto a implementação atual usa **Brazil**, na PDI dev457483; Zurich é o ambiente histórico. Conferir compatibilidade de recursos e caminhos de interface antes de aplicar instruções.

Entradas úteis:

- [Visão geral](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/aes-overview.md)
- [Criação de aplicações](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/aes-app-creation.md)
- [Criação de tabela](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/app-tutorial-create-table.md)
- [Configuração de tabela](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/app-tutorial-configure-table.md)
- [Segurança](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/add-security.md)
- [Teste de aplicação](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/app-tutorial-test-app.md)

## Documentação da implementação

Implementação atual Brazil: [Atividade 1 — Brazil](ATIVIDADE-1-BRAZIL.md). Entrega encerrada com documentação e exportações complementares publicadas em https://github.com/fredsons/mentorship-program . Histórico de commits e limites de preservação em [VERSIONAMENTO.md](VERSIONAMENTO.md).

Arquivo: [DOCUMENTACAO.md](HISTORICO-ZURICH.md).

Finalidade: registrar o que foi configurado, os motivos das decisões, os testes e os limites da implementação. Não substitui o enunciado nem uma exportação da aplicação.



## Revisão de fontes — 04/11/2026

Confirmados localmente: enunciados das quatro atividades, 78 slides e 137 arquivos Markdown do App Engine Studio. A branch oficial Brazil estava acessível, com head `31390e57c94e183d8e5293bc7e197913b9072bd6`; esse marco não significa que todos os tópicos foram auditados.

Documentação atual: [visão geral](../README.md), [Atividade 1](ATIVIDADE-1-BRAZIL.md), [Atividade 2 consolidada](ATIVIDADE-2-BRAZIL.md), [Atividade 3](ATIVIDADE-3-BRAZIL.md) e [Atividade 4 e extras](ATIVIDADE-4-BRAZIL.md).

Os documentos de execução registram capturas e confirmações do usuário; não equivalem à disponibilidade de cada captura original neste repositório nem a uma nova auditoria da instância. Os links da PDI exigem acesso ao ambiente. As fontes locais de imagens e a biblioteca Australia não são copiadas automaticamente para o GitHub.

Os links técnicos desta cópia publicada apontam para a referência oficial Brazil. A coleção local Australia e os arquivos de imagens permanecem no workspace; não foram incorporados ao repositório. O histórico Zurich está em HISTORICO-ZURICH.md.
