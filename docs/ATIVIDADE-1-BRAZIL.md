# Atividade 1 — Aplicação e Tabelas

Aplicação: Mentorship Program. Versão: Brazil. Instância: dev457483. Conclusão funcional: 29/10/2026.

Esta documentação descreve a reconstrução no escopo `x_2273184_mentor_0`. A documentação original da PDI Zurich é histórica e utiliza outro escopo. Os exemplos e identificadores abaixo pertencem à implementação Brazil.

## 1. Aplicação escopada

Criada pelo App Engine Studio com nome Mentorship Program e descrição Manage mentorship sessions. O escopo próprio reúne os componentes e permite versionar a aplicação separadamente.

O vínculo HTTPS com o repositório privado fredsons/mentorship-program foi configurado antes das tabelas, na branch main. O token foi inserido pelo usuário diretamente na credencial do ServiceNow; nenhum segredo faz parte desta documentação.

## 2. Cadastro de mentores

Mentor foi criada do zero, sem estender Task, pois representa um cadastro e o enunciado exige tabela independente.

| Campo | Tipo | Configuração e motivo |
|---|---|---|
| Name | Reference | User [sys_user]; reutiliza usuários existentes; Display para exibir o nome do mentor |
| Biography | String | Limite 1.000; descrição profissional |
| Expertise area | Choice | Financial, Health, IT, Marketing, Other; classificação padronizada |
| Available | True/False | Permite filtrar a seleção de mentores |
| Concluded Sessions | Integer | Padrão 0, configurado no Dictionary; contador disponível para etapas futuras |
| Number | String / Auto number | Prefixo MEN, início 1000, sete dígitos |

O formulário apresenta Number e Name à esquerda; Available, Expertise area e Concluded Sessions à direita; Biography em uma coluna de largura completa abaixo, integrada à seção anterior.

A lista principal contém Number, Name, Expertise area, Concluded Sessions e Available. O contador ainda não tem automação de atualização.

## 3. Sessões de mentoria

Mentorship Session foi criada estendendo Task, conforme a atividade. Isso aproveita Number, Opened by, Active, State, Short description, Description, Additional comments e Work notes.

| Campo próprio | Tipo | Motivo |
|---|---|---|
| Mentor’s Name (`mentors_name`) | Reference para Mentor | Vínculo com disponibilidade e especialidade do cadastro |
| Session Date (`session_date`) | Date/Time | Agendamento com data e hora |
| Session Feedback (`session_feedback`) | HTML | Feedback com formatação |

Auto number configurado com prefixo MTS, início 1000 e sete dígitos.

No topo do formulário: Number, Opened by e Mentor’s Name à esquerda; Active, State e Session Date à direita. Abaixo: Short description, Description, Additional comments, Session Feedback, Work notes e Activities (filtered).

O formatter foi adicionado por Configure → Form Layout. Em registro salvo, exibiu a nota de acompanhamento e as mudanças de campos.

## 4. Estados

| Estado | Valor |
|---|---:|
| Draft | 10 |
| Awaiting approval | 20 |
| Accepted | 30 |
| Rejected/Canceled | 40 |
| Done | 50 |

As choices foram configuradas no contexto da tabela de sessões. As opções antigas foram retiradas da seleção da tabela filha; o formulário novo passou a apresentar Draft. Não foi feita uma alteração global nos estados de Task.

Como State é herdado, um Dictionary Override para Mentorship Session define o padrão 10. Isso evita alterar o padrão das demais tabelas que utilizam Task.

## 5. Referências e listas relacionadas

Mentor’s Name utiliza Reference qual condition: Available is true. A Reference List contém Number, Name e Expertise area.

No mentor, foi adicionada Mentorship Session → Mentor’s Name. Criar uma sessão pela lista relacionada preencheu o mentor automaticamente. Na sessão, foi adicionada Approvers.

A lista principal e o layout da lista relacionada de sessões foram configurados com Number, Short description, Opened by, Mentor’s Name, Session Date, State, Created e Updated. Quando o campo de vínculo já é fixado pelo contexto relacionado, sua apresentação pode ser suprimida pela interface.

## 6. Exceção Global — layout de Approvers

A tabela Approval pertence ao Global. O editor scoped bloqueou a edição da Default view. Criar a view Mentorship Approvers no escopo não a aplicou ao formulário padrão. A tentativa de mudar diretamente a referência dessa view para Default view foi rejeitada e não foi tratada como alteração salva.

O ajuste efetivo utilizou Configure → List Layout → Edit this view in Global, no contexto da lista relacionada do formulário Mentorship Session. O resultado apresenta apenas State, Approver e Comments.

Esse layout Global foi exportado separadamente, com um registro sys_ui_list e três sys_ui_list_element. A view scoped adicional permanece sem uso confirmado; não foi removida automaticamente.

## 7. Menu e módulos tradicionais

Application Menu Mentorship Program, ativo, categoria Custom Applications, sem restrição de roles nesta etapa.

Foi utilizado o formulário tradicional por preferência do usuário. Nesta versão, o botão New podia redirecionar ao editor novo. Os módulos foram criados diretamente em `sys_app_module.do?sys_id=-1`, associados ao menu existente.

| Título | Ordem | Tipo | Tabela |
|---|---:|---|---|
| Mentorship Session | 100 | Separator | — |
| Create new | 110 | New Record | Mentorship Session |
| List | 120 | List of Records | Mentorship Session |
| Mentor | 200 | Separator | — |
| Create new | 210 | New Record | Mentor |
| List | 220 | List of Records | Mentor |

Os separadores agrupam criação e consulta por entidade. O menu final foi conferido na interface.

## 8. Permissões provisórias

Papéis padrão admin e user da aplicação. Na criação das tabelas, admin recebeu todas as operações e user recebeu leitura. O desenvolvimento e as verificações desta etapa foram realizados com System Administrator.

Essas permissões não representam a matriz definitiva da Atividade 2. Não foi afirmada validação de acesso de usuários comuns nesta etapa.

## 9. Validações e dados de teste

| Verificação | Evidência |
|---|---|
| Numeração de mentores | MEN0001006 e MEN0001007 |
| Numeração de sessões | MTS0001009 |
| Contador inicial | Formulário novo e XML dos mentores com 0 |
| Estado inicial | Nova sessão em Draft; XML com state=10 |
| Vínculo de sessão | MTS0001009 referencia Abel Tuter |
| Disponibilidade | Abel=true, Abraham=false; lupa mostrou somente Abel |
| Nome na referência | Abel Tuter exibido no formulário |
| Histórico | Nota “Primeiro registro de acompanhamento.” exibida e exportada |
| Approvers | Colunas State, Approver e Comments conferidas |
| Navegação | Dois grupos com Create new e List |

As exportações contêm dois mentores, uma sessão e uma nota sys_journal_field. Foram verificados os vínculos sessão→mentor e nota→sessão. Os registros completos dos usuários referenciados não estão nesses arquivos; devem existir ou ser mapeados na instância de destino.

## 10. Marcos de versionamento

| Commit | Conteúdo |
|---|---|
| 66d18e3 | Estado inicial da aplicação e vínculo com Git |
| 63f9c6c | Tabela Mentor, campos e formulário |
| 884eaa7 | Sessões, estados e relacionamentos |
| b922ea6 | Menu, seis módulos e lista principal de sessões |

Este fechamento acrescenta documentação e exportações complementares fora da pasta gerada pelo ServiceNow. Nenhum XML da aplicação foi editado manualmente para esse envio.

## 11. Critério de conclusão e limites

Atividade 1 concluída com base nas configurações, capturas e exportações verificadas. Foram entregues aplicação escopada, duas tabelas, campos, numeração, formulários, listas, estados, relacionamentos, seleção por disponibilidade, navegação e dados para teste.

O conjunto preservado não é backup integral da PDI. O teste de importação em outra instância não foi realizado e não é apresentado como concluído. A auditoria completa e os registros de usuários não foram exportados. A lista Approvers estava sem registros; criar o fluxo de aprovação não fazia parte desta atividade.

A Atividade 2 permanece como próxima etapa, dedicada à segurança e aos acessos. Automação de aprovação, atualização automática do contador e regras de conflito de horários não foram implementadas nesta entrega.

## Referências

- Enunciado local: cinco imagens da Atividade 1 disponibilizadas no projeto Shark Academy.
- Material de consulta: slides do bootcamp, sem ampliar os requisitos.
- [Documentação ServiceNow Brazil](https://github.com/ServiceNow/ServiceNowDocs/tree/brazil).
- [Vínculo com Source control](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/source-control-link-application.md).
- [Pull from repository](https://github.com/ServiceNow/ServiceNowDocs/blob/brazil/markdown/application-development/app-engine-studio/source-control-apply-changes.md).
