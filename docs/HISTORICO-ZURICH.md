# Documentação — Mentorship Program

**Índice atual (04/11/2026):** [visão geral Brazil](../README.md), [Atividade 1](ATIVIDADE-1-BRAZIL.md), [Atividade 2](ATIVIDADE-2-BRAZIL.md), [Atividade 3](ATIVIDADE-3-BRAZIL.md) e [Atividade 4 e extras](ATIVIDADE-4-BRAZIL.md). O conteúdo Zurich abaixo é histórico e foi preservado.

Fontes e material de consulta: [FONTES.md](FONTES.md). A pasta de slides é referência de apoio e não amplia os requisitos da atividade.

**Registro histórico da implementação Zurich.** A reconstrução e conclusão na PDI Brazil estão documentadas em [Atividade 1 — Brazil](ATIVIDADE-1-BRAZIL.md), com preservação registrada em [VERSIONAMENTO.md](VERSIONAMENTO.md). Os nomes técnicos abaixo pertencem à PDI original e não devem ser copiados diretamente para a nova aplicação.

Plataforma: ServiceNow Zurich  
Atividade: 1 — Aplicação e Tabelas  
Data: 28/10/2026

## 1. Objetivo e origem

A aplicação cadastra mentores e acompanha sessões de mentoria. Esta documentação registra as configurações e os testes apresentados nas capturas de tela durante a implementação, com base nas cinco imagens do enunciado da Shark Academy.

O objetivo desta etapa é preparar dados, formulários, relacionamentos e navegação. Automações de aprovação e de contagem de sessões não foram solicitadas nesta atividade.

## 2. Criação da aplicação

Criada pelo App Engine Studio como aplicação escopada:

- Nome: Mentorship Program.
- Descrição: Manage mentorship sessions.
- Prefixo técnico gerado: `x_2281079_mentor_0_`.

O escopo reúne tabelas, campos, papéis e módulos do projeto e distingue seus componentes das configurações globais.

## 3. Modelo de dados

| Tabela | Nome técnico | Origem |
|---|---|---|
| Mentor | `x_2281079_mentor_0_mentor` | Criada do zero |
| Mentorship Session | `x_2281079_mentor_0_mentorship_session` | Extensão de Task |

Um mentor pode ter várias sessões. Cada sessão referencia um mentor.

## 4. Tabela Mentor

Foi criada sem herdar outra tabela, conforme o enunciado. Mentor é um cadastro de profissionais e não precisa dos campos de tarefa.

| Campo | Nome técnico | Tipo e configuração |
|---|---|---|
| Name | `name` | Reference para User [sys_user]; Display da tabela |
| Biography | `biography` | String; máximo de 1.000 caracteres |
| Expertise area | `expertise_area` | Choice |
| Available | `available` | True/False |
| Concluded Sessions | `concluded_sessions` | Integer; padrão 0 |
| Number | `number` | String com numeração automática |

Name aproveita usuários existentes. Foi marcado como Display para que referências ao mentor mostrem seu nome. O comportamento foi confirmado com Abel Tuter.

Expertise area contém Financial, Health, IT, Marketing e Other. As opções padronizam a classificação e foram conferidas no formulário.

Available indica se o mentor pode ser selecionado em uma sessão.

Concluded Sessions começa com zero. O editor do App Engine Studio rejeitou zero, então o padrão foi definido em Configure Dictionary → Default Value. Um novo formulário confirmou o preenchimento automático. Não existe atualização automática desse contador nesta etapa.

## 5. Tabela Mentorship Session

Foi criada a partir da tabela extensível Task, conforme a atividade. Isso permite aproveitar Number, Opened by, Active, State, Short description, Description, Additional comments e Work notes.

| Campo próprio | Nome técnico | Tipo |
|---|---|---|
| Mentor’s Name | `mentors_name` | Reference para Mentor |
| Session Date | `session_date` | Date/Time |
| Session Feedback | `session_feedback` | HTML |

A sessão referencia Mentor porque disponibilidade e especialidade pertencem a esse cadastro. A referência ao usuário já existe dentro de Mentor. Date/Time registra o agendamento completo; HTML permite feedback formatado e atende ao tipo solicitado.

## 6. Numeração automática

Habilitada nas duas tabelas. Exemplos confirmados: MEN0001002 e MTS0001015.

Na tabela de sessões, MEN já estava em uso, então foi utilizado MTS, com número inicial 1000 e sete dígitos. A atividade permite escolher os parâmetros. Os identificadores distinguem os registros e facilitam sua consulta.

## 7. Formulário de Mentor

| Coluna esquerda | Coluna direita |
|---|---|
| Number | Available |
| Name | Expertise area |
| | Concluded Sessions |

Biography ocupa uma coluna de largura completa abaixo dos demais campos. O layout segue o modelo e oferece mais espaço ao texto da biografia.

## 8. Formulário de sessão e Activities

| Coluna esquerda | Coluna direita |
|---|---|
| Number | Active |
| Opened by | State |
| Mentor’s Name | Session Date |

Abaixo, em uma coluna: Short description, Description, Additional comments, Session Feedback, Work notes e Activities.

O formatter disponível na interface Zurich foi Activities (filtered). Foi incluído pela interface clássica em Configure → Form Layout, após Work notes. O teste em registro salvo apresentou a nota “Primeira nota de teste” e alterações de campos.

O componente permite acompanhar o histórico. A interface reorganizou a entrada de comentários e notas no registro salvo. O teste exigiu salvar e reabrir uma sessão; a ausência do histórico em um formulário novo não comprovava falha.

## 9. Estados e Dictionary Override

| Estado | Valor | Sequência |
|---|---:|---:|
| Draft | 10 | 0 |
| Awaiting approval | 20 | 1 |
| Accepted | 30 | 2 |
| Rejected/Canceled | 40 | 3 |
| Done | 50 | 4 |

Os valores numéricos distintos foram escolhidos para esta implementação. A atividade não determina números específicos.

Como State é herdado de Task, foi criado um Dictionary Override:

- Base table: Task.
- Table: Mentorship Session.
- Column name: state.
- Override default value: marcado.
- Default value: 10.

Isso define Draft como padrão apenas para as sessões, preservando o padrão global de Task.

As choices foram configuradas para `x_2281079_mentor_0_mentorship_session`. A consulta final mostrou cinco registros ativos, valores 10 a 50 e sequência 0 a 4. O formulário mostrou somente essas opções e um novo registro iniciou em Draft.

Não houve desativação global dos estados de Task. O enunciado pede que as opções herdadas sejam desativadas; a evidência funcional confirma sua ausência no formulário da sessão. A captura final comprova as cinco choices ativas da tabela filha, sem comprovar registros antigos inativos nessa tabela.

## 10. Seleção e disponibilidade do mentor

Em Mentor’s Name → Configure Dictionary → Reference Specification, foi aplicada a condição Available is true.

Motivo: permitir selecionar apenas mentores disponíveis.

Teste realizado:

| Mentor | Available | Resultado na lupa |
|---|---|---|
| Abel Tuter | true | Apareceu |
| Abraham Lincoln | false | Não apareceu |

A visualização Reference List foi configurada com Number, Name e Expertise area, nessa ordem. Ela apresenta identificação e especialidade antes da seleção. A exibição do nome selecionado foi confirmada.

## 11. Listas relacionadas

No formulário Mentor foi adicionada Mentorship Session → Mentor’s Name. Ela mostra as sessões que referenciam o mentor. Ao usar New nessa lista, Mentor’s Name veio preenchido com Abel Tuter. A sessão MTS0001015 foi salva e apareceu no cadastro dele.

No formulário da sessão foi adicionada Approvers, com State, Approver e Comments. A coluna adicional Created foi removida para seguir o modelo. A lista ficou vazia porque não foram cadastradas aprovações. Adicionar a lista não cria um fluxo automático.

## 12. Layout das listas

Mentor: Number, Name, Expertise area, Concluded Sessions e Available.

Mentorship Session: Number, Short description, Opened by, Mentor’s Name, Session Date, State, Created e Updated.

Biography foi removida da lista principal de mentores conforme o modelo. Uma personalização pessoal inicialmente sobrepunha o layout padrão. A restauração das colunas padrão resolveu a diferença; a captura seguinte confirmou a ordem correta.

As configurações da lista principal de sessões e da lista relacionada foram conferidas durante os testes.

## 13. Menu e módulos

Application Menu criado no escopo Mentorship Program:

- Title: Mentorship Program.
- Active: marcado.
- Category: Custom Applications.
- Hint: Manage mentors and mentorship sessions.
- Description: Manage mentors and track mentorship sessions.
- Roles: sem restrição adicional nesta etapa.

| Título | Ordem | Link type | Tabela |
|---|---:|---|---|
| Mentorship Session | 100 | Separator | — |
| Create new | 110 | New Record | Mentorship Session |
| List | 120 | List of Records | Mentorship Session |
| Mentor | 200 | Separator | — |
| Create new | 210 | New Record | Mentor |
| List | 220 | List of Records | Mentor |

Os módulos organizam criação e consulta por tabela. Os valores de ordem mantêm cada grupo junto de suas opções. O menu foi exibido e utilizado nos testes.

## 14. Papéis e permissões

O assistente gerou os papéis admin e user da aplicação. Durante a criação das tabelas, a orientação foi conceder todas as operações ao papel admin e leitura ao papel user. O enunciado permite deixar o aprofundamento de permissões para depois.

Os testes foram realizados com System Administrator. Não foi feita validação com usuário comum portador apenas do papel da aplicação; portanto, esta documentação não certifica o comportamento completo das ACLs.

## 15. Evidências de validação

- Numeração automática nas duas tabelas.
- Novo mentor com Concluded Sessions igual a zero.
- Nova sessão com State igual a Draft.
- Cinco estados disponíveis e choices de especialidade conferidas.
- Nome do mentor exibido nas referências.
- Sessão criada pela lista relacionada com mentor preenchido.
- Sessão MTS0001015 vinculada a Abel Tuter.
- Mentor indisponível excluído da seleção.
- Reference List com três colunas conforme o modelo.
- Histórico com nota de trabalho e alterações de campos.
- Approvers disponível no formulário.
- Listas e menu conferidos nas capturas.

## 16. Limites e próximas etapas

Não foram implementados fluxo automático de aprovação, atualização automática do contador, prevenção de conflitos de horário, regras adicionais de obrigatoriedade ou testes completos de acesso por perfil. Esses recursos exigem requisitos próprios e não integram o escopo apresentado da Atividade 1.

A estrutura permite cadastrar mentores, selecionar os disponíveis, registrar sessões e consultar seu estado e histórico. As evidências demonstram o atendimento funcional dos requisitos apresentados, com a ressalva documental sobre a desativação literal das choices herdadas descrita na etapa 9.

## Atualização documental — Atividade 4 e extras (01/11/2026)

- [Mentorship Program: Atividade 4 e extras](ATIVIDADE-4-BRAZIL.md): Record Producer, Employee Center, critérios de acesso, UI Policies, indicador de etapas e validação de datas, com distinção entre configuração, testes e preservação.
- A documentação corresponde à PDI dev457483, versão Brazil, escopo x_2273184_mentor_0. Esses identificadores não se aplicam automaticamente a outras aplicações do bootcamp.
- Equipment Loan Management permanece separado e depende de suas próprias evidências para consolidação documental.

