# Versionamento — Shark Academy

## Estado consolidado — 04/11/2026

As quatro atividades e os extras de Mentorship Program estão implementados e documentados. Ambiente atual: dev457483, Brazil, escopo `x_2273184_mentor_0`. O histórico abaixo preserva as pendências existentes em cada data; elas não devem ser interpretadas como pendências atuais quando houver marco posterior.

### Atividade 4 e extras — commits conferidos no GitHub

| Marco | Commit |
|---|---|
| Record Producer, grupos e Employee Center | `2f66b9616445d6c4d664b5a41c691f8686f43599` |
| Obrigatoriedade, feedback, fases, menu e data | `dbe11f71cb27956a14dc401c54eaae29a1d8d768` |
| Melhoria visual da data no portal | `227e9bb575a97ce016c5f66c6cf3cc369946c670` |
| README atualizado em 04/11 | `9e151bfe50430160c3a09abd8f4847a896822022` |

MTS0001019 foi criada pelo portal, aprovada e observada em Accepted. Os XMLs de dados listados mais recentes continuam sendo os da Atividade 3. Exportação dos dados da Atividade 4 e conferência de componentes Global/outros escopos permanecem sem confirmação. A PDI antiga dev435099 (Zurich) foi liberada pelo usuário. A restauração em outra PDI não foi testada e não está planejada; não integra as pendências do projeto. Essa decisão atual substitui as expectativas históricas de recuperação registradas abaixo. A revisão atual publica documentação; não altera a aplicação na PDI nem gera novos exports.

Após alterações documentais externas, sincronizar a PDI por Pull from repository antes de novos commits, preservando mudanças locais. Markdown e exports fora da pasta nativa não viram registros da plataforma.

## Contexto histórico em 29/10/2026

Shark Academy reúne as atividades do bootcamp e pode conter várias aplicações. Mentorship Program é a primeira aplicação; sua documentação da Atividade 1 está em DOCUMENTACAO.md e descreve a implementação original em Zurich.

- PDI original: dev435099, Zurich. Foi liberada pelo usuário, conforme confirmação em 04/11/2026; sem exportação confirmada dessa implementação. A expectativa anterior de recuperação foi encerrada.
- PDI da reconstrução: dev457483, Brazil. Atividade 1 concluída com tabelas, formulários, listas, referências, menu, validações e exportações complementares publicadas no GitHub. Controle de versão ativo; papéis e acessos definitivos da Atividade 2 ainda pendentes.
- Conta GitHub conectada identificada: fredsons.

## Organização acordada

Manter um repositório dedicado aos arquivos da aplicação Mentorship Program, integrado ao Source control do ServiceNow.

Repositório criado e conferido em 29/10/2026: https://github.com/fredsons/mentorship-program . Visibilidade privada e branch main. URL HTTPS de integração: `https://github.com/fredsons/mentorship-program.git`. Autenticação e vínculo com a PDI concluídos; primeiro commit confirmado pela API do GitHub.

### Primeiro marco confirmado

- Aplicação: Mentorship Program, sys_id `540f96e483945750e9c7f2d6feaad334`.
- Escopo confirmado no XML da nova aplicação: `x_2273184_mentor_0` (diferente do escopo da PDI Zurich).
- Commit: `66d18e3acfb44cfbd91942dd66c4a5909586f134`.
- Mensagem: `Initial state of application at link to source control`.
- Link: https://github.com/fredsons/mentorship-program/commit/66d18e3acfb44cfbd91942dd66c4a5909586f134 .
- Raiz verificada: diretório da aplicação e `sn_source_control.properties`.
- Diretório da aplicação verificado: `README.md`, `checksum.txt`, XML de `sys_app` e pasta `update`.
- O commit preserva o estado inicial da nova aplicação. A reconstrução das tabelas e demais configurações da Atividade 1 ainda precisa ocorrer.

A documentação geral do bootcamp pode ser versionada em um repositório Shark Academy separado. Isso não deve misturar aplicações ServiceNow distintas no mesmo repositório de integração.

## Próximos passos

### Marco Mentor — confirmado em 29/10/2026

- Commit: `63f9c6c989fafd2285d68e56457d856b814c2f92`.
- Mensagem: `Cria tabela Mentor com campos e formulário`.
- Link: https://github.com/fredsons/mentorship-program/commit/63f9c6c989fafd2285d68e56457d856b814c2f92 .
- Confirmado pela API na branch main: 29 arquivos no commit, incluindo definição de tabela, dicionário dos campos, choices de especialidade, formulário e permissões iniciais. Os 27 itens selecionados no assistente correspondem a registros da aplicação; o commit também contém arquivos auxiliares gerados.
- Formulário novo apresentado nas capturas: numeração MEN, campos organizados em duas colunas, Biography em largura completa e Concluded Sessions exibindo 0.
- A captura do GitHub confirmou main como branch padrão após correção da branch undefined.
- Pendentes na ocasião desse marco: layout da lista Mentor, tabela Mentorship Session e demais requisitos da Atividade 1. Os marcos seguintes registram sua evolução. Atividade 2 ainda não implementada nesta PDI.

### Marcos seguintes

### Reconstrução da sessão e ajuste de Approvers — evidências de 29/10/2026

As capturas confirmam a criação de Mentorship Session, os três campos próprios, formulário, formatter Activities, estado inicial Draft, condição Available is true no campo de mentor, Reference List com Number/Name/Expertise area e listas relacionadas. A sessão de teste MTS0001009 foi vinculada ao mentor Abel Tuter (MEN0001006), e o histórico exibe a nota de trabalho gravada. O teste de disponibilidade foi posteriormente validado pela captura da lupa e pelas exportações, conforme os marcos seguintes.

A lista Approvers foi ajustada para State, Approver e Comments. A criação de uma view scoped chamada Mentorship Approvers não alterou a lista exibida no formulário Default view. A tentativa de reassociar esse sys_ui_list à Default view foi rejeitada por restrição de escopo da tabela Approval; não considerar a tentativa como atualização salva.

O ajuste funcional foi realizado pelo próprio editor: Configure → List Layout → Edit this view in Global. O cabeçalho indicava o contexto da lista relacionada no formulário Mentorship Session. Foram removidas Approval for e Created do layout, e a captura posterior confirmou as três colunas esperadas.

**Exportação concluída e validada:** registros Global preservados em `exports/mentorship-program/brazil/global-approvers/approvers-layout-global.xml` e `approvers-layout-elements.xml`. Confirmados um registro sys_ui_list e três sys_ui_list_element associados ao mesmo layout, com state=0, approver=1 e comments=2. Publicados separadamente no commit de fechamento abaixo; não fazem parte da carga automática scoped. Teste de restauração ainda não executado. A view adicional Mentorship Approvers permanece sem uso confirmado; revisar posteriormente, sem excluir automaticamente.

**Commit confirmado pela API em 29/10/2026:** `884eaa79b323069969ea1de701f423ec13d46bc0`, mensagem `Configura sessões de mentoria, estados e relacionamentos`, na main. A resposta apresentou 33 arquivos; entre eles estão o Dictionary Override, as listas Mentor/default e Mentor/reference, o layout da lista relacionada de sessões no mentor e as definições das listas relacionadas. Link: https://github.com/fredsons/mentorship-program/commit/884eaa79b323069969ea1de701f423ec13d46bc0 .

O layout de aprovações presente nesse commit corresponde à view `mentorship_approvers`, criada no escopo. A lista de arquivos apresentada não contém o layout Global/Default view em uso; posteriormente, sua exportação separada foi concluída localmente, conforme registro acima.

### Marco menu e lista principal — confirmado em 29/10/2026

- Commit: `b922ea6e54b90bc8489e85c68a59c357b131e513`.
- Mensagem: `Configura menu da aplicação e lista principal de sessões`.
- Link: https://github.com/fredsons/mentorship-program/commit/b922ea6e54b90bc8489e85c68a59c357b131e513 .
- Confirmados no commit: seis arquivos de módulos, configuração do menu e layout da lista principal de sessões.
- Navegação conferida por captura: Mentorship Program → Mentorship Session (Create new, List) e Mentor (Create new, List).
- Preferência do usuário: utilizar o formulário tradicional para menus e módulos. Nesta PDI, New pode redirecionar ao editor novo; acesso direto ao formulário: `sys_app_module.do?sys_id=-1`.
- Lista principal de sessões configurada com Number, Short description, Opened by, Mentor’s Name, Session Date, State, Created e Updated.
- Após cadastro de um mentor indisponível, a captura da lupa exibiu somente Abel Tuter. A exportação posterior confirmou Abraham Lincoln com available=false e Abel com available=true, validando o teste em conjunto com a captura.
- Exportações posteriores dos dados validadas e preservadas em `exports/mentorship-program/brazil/data/`: dois mentores, uma sessão e uma nota de trabalho. Vínculos sessão→mentor e nota→sessão consistentes. Os arquivos complementares foram publicados no commit de fechamento abaixo.

### Fechamento da Atividade 1 — publicado e verificado em 29/10/2026

- Commit: `92866676f081cb70c17be46af8701713d159afbb`.
- Link: https://github.com/fredsons/mentorship-program/commit/92866676f081cb70c17be46af8701713d159afbb .
- Mensagem: `Conclui atividade 1 com documentação Brazil e exportações complementares`.
- Oito arquivos acrescentados à main: README principal, documentação da Atividade 1 Brazil, quatro XMLs complementares e dois READMEs de exportação.
- Validação remota: SHA de cada arquivo novo conferido; todos os arquivos anteriores preservados sem alteração; main apontando para o commit de fechamento.
- Documentação atual local: `ATIVIDADE-1-BRAZIL.md`. Cópia publicada em `docs/ATIVIDADE-1-BRAZIL.md`. README local em `../README.md`, publicado como README.md da raiz do repositório.
- Entrega funcional da Atividade 1 encerrada. Importação/restauração em outra instância não testada; usuários referenciados e auditoria completa não integram os XMLs.
- Como esse commit foi criado fora da PDI, sincronizar o Source control pelo menu Pull from repository antes do próximo ciclo de desenvolvimento. Preservar mudanças locais caso existam; não descartá-las para resolver divergências.

### Rotina

1. Concluído: criar repositório privado dedicado no GitHub, inicialmente vazio.
2. Concluído: usuário preparou autenticação e inseriu a credencial diretamente no ServiceNow. Nenhum segredo foi registrado nesta documentação.
3. Concluído: vínculo pelo App Engine Studio → Source control → Link to source control.
4. Concluído: primeiro commit e arquivos confirmados no GitHub; reconstrução das tabelas pode ser retomada.
5. Registrar alterações em commits conforme cada etapa for validada.
6. Exportar a aplicação e os dados de teste separadamente, como proteção adicional.

O controle de versão da aplicação não deve ser presumido como backup completo da PDI, de credenciais ou de todos os dados de negócio. Os marcos de configuração estão confirmados; layout Global e dados de teste foram exportados, validados e publicados como complementos no GitHub. Teste de restauração ainda não executado. O envio de alterações futuras exige novos commits pelo Source control; não presumir sincronização contínua automática.

## Referências consultadas

- fontes/app-engine-studio/source-control-link-application.md: orienta um repositório dedicado, acesso de leitura/escrita e o vínculo pelo App Engine Studio. A cópia local é da versão Australia; conferir a interface Brazil durante o procedimento.
- Confirmado também no arquivo oficial da branch Brazil: https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/source-control-link-application.md (blob consultado: 1feafe3ad89bb7860164bfc4d3e7f4fc7c2d67a0).
- https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens : autenticação por token, com preferência por escopo mínimo e seleção de repositórios quando aplicável.
# Marco da Atividade 2 — 30/10/2026

Marco mais recente: configuração de State confirmada no commit `24da2ded4a6e087bd28b9fea063efaeb4a285f3d`; documentação consolidada e exportação final em `e0bb032476e4b7a9ebefff66e3ece0620c320826`, com head main conferido. Total atual: 2 roles e 19 ACLs ativas. MTS0001015 exportada em Accepted (30), atualizada por abel.tuter; dois registros de sessão e três journals preservados. Sessão temporária MTS0001016 criada/excluída como mentor, confirmada pelo usuário e ausente da exportação final. Verificação das árvores mostrou cinco arquivos complementares alterados, sem alteração em arquivos nativos pelo commit de documentação. Referência consolidada: `ATIVIDADE-2-BRAZIL.md`, publicada como `docs/ATIVIDADE-2-BRAZIL.md`. Os marcos abaixo são históricos.

Preservação complementar enviada e head conferido: `dd69f20b8ba6b3708d8b7312e1fd222f3aeeb55c`. Dez arquivos de documentação/exportações alterados; pasta nativa da aplicação preservada integralmente. Inclui 2 grupos, 2 vínculos de roles, 5 membros, 4 mentores, 2 sessões e 3 journals. Restauração e cenários funcionais pendentes continuam documentados. Sincronizar a PDI por Pull from repository antes de novos commits, preservando eventuais mudanças locais.

Captura do AES confirmou envio bem-sucedido ao source control do commit `7d33fb0f2c064f94daf6445b34b8fc5134096c7b`, com 67 arquivos selecionados. Estado observado: duas roles do escopo, 18 ACLs ativas, exclusão de dez ACLs provisórias e das roles iniciais admin/user do escopo, menus por perfil e testes descritos em `ATIVIDADE-2-BRAZIL.md`.

Exportações anteriores à limpeza preservadas em `exports/mentorship-program/brazil/security/2026-10-30-before-cleanup/`. Documentação local atualizada nesta etapa ainda não enviada ao GitHub. Grupos, membros, atribuições e novos dados de teste ainda precisam de preservação complementar; não interpretar o commit como backup integral da PDI.

## Marco da Atividade 3 — 30/10/2026

Fechamento publicado e main verificada: `5406740503121da129f4ad644711adcb1bc5a10b`. Seis arquivos complementares alterados, sem mudança na pasta nativa: documentação, README, três XMLs e README das exportações. Conjunto atual: 4 mentores, 4 sessões, 2 aprovações e 8 journals incorporados (7 sessões, 1 aprovação). MTS0001017 Done/approved; MTS0001018 Rejected-Canceled/rejected; Abel contador 1. Usuários, auditoria completa e contextos de execução não exportados; restauração não testada. Falta sincronizar a PDI com Pull from repository após este commit externo.

Documentação e README publicados em `faefa378b7e5835da071a4235e23e97baeb8cd34`. Diff verificado: somente README.md e docs/ATIVIDADE-3-BRAZIL.md; arquivos nativos preservados. Sincronizar a PDI via Pull from repository antes de novas alterações. Dados complementares ainda pendentes.

Configuração nativa confirmada em `40346b001294a112f3b2dbfbe4cfc009a2a4a268`: fluxo `ee491b30831cd750e9c7f2d6feaad3b8` ativo/publicado, Run As System User, e Session Feedback HTML com Max length 4000. MTS0001017 aprovada e concluída; contador Abel 0→1. MTS0001018 rejeitada com comentário; State Rejected/Canceled e contador mantido em 1. Exportações atuais de dados/aprovações ainda pendentes. Documentação em `ATIVIDADE-3-BRAZIL.md`.

## README consolidado — 30/10/2026

README principal reescrito para apresentar toda a aplicação, atividades 1 a 3, modelo de dados, segurança, fluxo, testes e preservação. Commit `97ae9ac4bb9d200f158e66c6ed7dcbc9dac0c66b`, head main verificada. Diff remoto limitado a README.md; metadados e exportações preservados. Cópia local sincronizada em ../README.md. Próxima atividade ainda sem enunciado. Após este commit externo, sincronizar a PDI por Pull from repository.


