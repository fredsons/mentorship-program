# Atividade 2 — Segurança e Acessos — Brazil

## Ambiente e requisitos

Aplicação Mentorship Program, PDI dev457483, escopo `x_2273184_mentor_0`. Requisitos extraídos das três imagens da Atividade 2 fornecidas pela Shark Academy. A configuração foi enviada pelo AES no commit `7d33fb0f2c064f94daf6445b34b8fc5134096c7b`.

Ajuste final de State enviado no commit `24da2ded4a6e087bd28b9fea063efaeb4a285f3d`, confirmado no GitHub: uma ACL de campo write e dois vínculos de roles. O estado atual é **duas roles e 19 ACLs ativas**. A exportação final de sessões confirma MTS0001015 em Accepted (30), atualizada por abel.tuter.

| Tabela | Operação | mentee | mentor |
|---|---|---|---|
| Mentorship Session | Create/Read | Sim | Sim |
| Mentorship Session | Write | Somente sessões criadas pelo próprio usuário; nunca Session Feedback | Sim |
| Mentorship Session | Delete | Não | Sim |
| Mentor | Create/Delete | Não | Sim |
| Mentor | Read | Sim | Sim |
| Mentor | Write | Não | Somente seu cadastro, identificado por Name |

## 1. Roles e grupos

Foram criadas as roles `.mentee` e `.mentor`, sem privilégio elevado, e atribuídas aos grupos Mentorados e Mentores, respectivamente. Essa organização permite gerenciar acesso por associação ao grupo, sem distribuir a role manualmente a cada usuário.

- Mentorship Program - Mentorados: Aileen Mottern e Adela Cervantsz.
- Mentorship Program - Mentores: Scott Seixas, Fred Luddy e Abel Tuter.

Scott e Fred possuem admin global e não servem para validar as restrições das ACLs com Admin overrides. Os testes de restrição foram realizados com Aileen e Abel, sem admin. Suas outras roles existentes não foram removidas.

## 2. ACLs de tabela

O AES criou as permissões por operação e perfil. As ACLs write restritas foram ajustadas em Data Condition:

- Mentor/mentor: **Name is (dynamic) Me OR Created is empty**. Name referencia sys_user; a identidade do mentor é diferente da autoria do cadastro. A exceção para Created vazio permite preencher o registro novo.
- Mentorship Session/mentee: **Created by is javascript:gs.getUserName() OR Created is empty**. A comparação usa o login do criador real, armazenado em sys_created_by, e permite o preenchimento antes da primeira gravação.

A segunda condição contém uma expressão JavaScript curta, embora Advanced permaneça desmarcado. Não é uma solução integralmente no-code. Created by é texto e não ofereceu o operador dinâmico Me na PDI. Foi investigada uma alternativa declarativa envolvendo Opened by, seu User ID e comparação entre campos; ela não foi implementada. O usuário escolheu a expressão direta pela simplicidade. A preferência do projeto permanece no-code quando atender ao requisito completo.

## 3. ACLs de campos herdados e feedback

Passar pela ACL da tabela não concede automaticamente acesso aos campos herdados de Task. O enunciado já previa a necessidade de regras para esses campos. Foram criadas ACLs específicas na tabela filha, preservando as regras globais de Task:

| Campo | Operação | Roles |
|---|---|---|
| short_description | write | mentee, mentor |
| description | write | mentee, mentor |
| comments | write | mentee, mentor |
| work_notes | write e read | mentee, mentor |
| session_feedback | write | mentor |
| state | write | mentee, mentor |

As condições dessas regras de campo ficam vazias; a regra de autoria continua na ACL da tabela. Session Feedback exige mentor tanto no formulário novo quanto no salvo, conforme os testes observados. Work notes precisou também de read para ficar disponível ao perfil de teste.

## 4. Menu e módulos

O menu Mentorship Program exige mentee ou mentor. O módulo Mentor/Create new, ordem 210, exige somente mentor, sem override das roles do menu. Os demais módulos utilizam o acesso do menu. Capturas por impersonação confirmaram:

- Mentee: criar/listar sessões e somente listar mentores.
- Mentor: criar/listar nas duas seções.

As roles dos módulos controlam a navegação; a proteção dos dados continua nas ACLs.

## 5. Limpeza das permissões provisórias

Foram revisadas 28 ACLs e 33 vínculos Requires role por sys_id. Dez ACLs usavam exclusivamente as roles iniciais `.admin` ou `.user` do escopo: oito para admin e duas para user. Foram desativadas, os testes próprios/alheios foram repetidos e depois as dez foram excluídas. As duas roles iniciais foram excluídas após conferir atribuições a usuários/grupos e as listas relacionadas disponíveis. Nenhuma role admin global dos usuários foi removida.

Estado confirmado por capturas: **duas roles e 18 ACLs ativas**. O commit do AES inclui as exclusões. O XML anterior à limpeza é histórico e não deve ser importado junto da configuração atual, pois reintroduziria regras retiradas.

Esse total de 18 corresponde ao marco inicial após a limpeza. A ACL específica de State acrescentada na validação final elevou o total para **19**.

## 6. Testes e evidências observadas

| Perfil | Verificação | Resultado |
|---|---|---|
| Abel/mentor | Edição do próprio Mentor | Formulário editável; alteração de Biography apresentada |
| Abel/mentor | Edição de Fred | Somente leitura, sem Update |
| Abel/mentor | Criar Mentor temporário para Adela | Criado MEN0001013; bloqueado para edição posterior por pertencer a Adela |
| Abel/mentor | Excluir Mentor temporário | Excluído; ausente da exportação |
| Aileen/mentee | Criar sessão | Criada MTS0001015 |
| Aileen/mentee | Editar a própria sessão | Description atualizada e persistida no XML |
| Aileen/mentee | Editar MTS0001009, de admin | Somente leitura, sem Update |
| Aileen/mentee | Session Feedback na sessão nova e própria salva | Bloqueado |
| Aileen/mentee | Additional comments e Work notes | Publicados e presentes nos journals exportados |
| Abel/mentor | Feedback em sessão de Aileen | Salvo e presente no XML |
| Ambos | Menu por perfil | Confirmado conforme item 4 |
| Abel/mentor | Criar e excluir sessão temporária | MTS0001016 criada com dados salvos; exclusão confirmada pelo usuário |
| Aileen/mentee | Editar e excluir Mentor | Cadastro de Abel somente leitura, sem Update/Delete |
| Aileen/mentee | Navegação para criar Mentor | Módulo Create new ausente; a borda direita da captura da lista não permitiu conferir o botão New |
| Aileen/mentee | Alterar State da sessão própria | Draft → Awaiting approval salvo e registrado no histórico |
| Aileen/mentee | Alterar State da sessão do administrador | Bloqueado, sem Update |
| Abel/mentor | Alterar State da sessão de Aileen | Awaiting approval → Accepted salvo e registrado no histórico |

Limites: a contagem de ACLs não substitui testes. A validação foi manual pela interface, por impersonação. Não houve teste de restauração ou de acesso por API, nem tentativa direta de criação de Mentor por URL como mentee. A ausência de Update/Delete é evidência da restrição na interface, não uma execução de operações por API. Os testes de State fecharam o bloqueio encontrado nos campos herdados; não se afirma que todos os campos herdados de Task foram liberados. Campos de identificação, por exemplo, permaneceram somente leitura.

## 7. Preservação e recuperação

- `exports/mentorship-program/brazil/groups/`: dois grupos, duas atribuições de roles e cinco membros.
- `exports/mentorship-program/brazil/data/atividade-2-2026-10-30/`: quatro mentores, duas sessões e três journals. O XML de sessões já incorpora os mesmos três journals do arquivo separado.
- `exports/mentorship-program/brazil/security/2026-10-30-before-cleanup/`: cópia histórica local das 28 ACLs e seus 33 vínculos, com inventário CSV. Não representa o estado final de 19 ACLs e não foi publicada no commit complementar; o histórico nativo do Git preserva as alterações e exclusões.
- Exportações da Atividade 1 e da lista Global de Approvers permanecem preservadas nos seus diretórios históricos.

Instalar primeiro a aplicação e suas roles; conferir usuários e sys_ids; importar grupos e vínculos e, depois, mentores e sessões. Os XMLs referenciam usuários existentes, mas não exportam seus cadastros. Não importar manualmente a cópia anterior à limpeza sobre a aplicação atual. A documentação e os XMLs fora da pasta nativa são arquivos de referência: Pull from repository não os transforma em registros da plataforma.

## Referências

- Enunciado: imagens 1, 2 e 3 da Atividade 2, fornecidas pelo usuário.
- [ACL types — documentação oficial](https://www.servicenow.com/docs/r/platform-security/access-control/acl-rule-types.html): avaliação de tabela/campo e herança.
- [Explore Access Control Lists — documentação oficial](https://www.servicenow.com/docs/r/platform-security/access-control/exploring-access-control-list.html): condições, operações e comportamento de registros novos.

