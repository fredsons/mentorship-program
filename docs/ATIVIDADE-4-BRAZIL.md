# Atividade 4 e extras — Catálogo e portal

Documentação consolidada em 04/11/2026; registros de execução de 01/11/2026 com base nas configurações e nos testes confirmados por capturas durante a execução manual.

Ambiente: PDI `dev457483`, versão Brazil, aplicação Mentorship Program, escopo `x_2273184_mentor_0`. A documentação Zurich descreve a implementação histórica.

## Requisitos e resultado

A Atividade 4 pede um Record Producer para criar sessões pelo Employee Center, com variáveis mapeadas para a tabela Mentorship Session, acesso limitado aos dois grupos da aplicação e um item no menu do portal.

O texto do slide menciona três variáveis, mas a imagem apresenta quatro. Foram implementadas as quatro da imagem: assunto, descrição, data e mentor. Assunto, data e mentor são obrigatórios; descrição é opcional. Não foi necessário associar o produtor a um catálogo ou categoria.

Os extras implementados são: impedir datas anteriores a hoje, tornar três campos obrigatórios no formulário sem alterar o dicionário, exibir feedback somente nos estados Accepted e Done, mostrar indicadores das fases e limitar a visibilidade do menu do portal. Também foi melhorada a mensagem de data inválida antes do envio pelo portal.

## 1. Record Producer

Foi criado o produtor **Mentorship Session**, ativo, na aplicação Mentorship Program, direcionado à tabela `x_2273184_mentor_0_mentorship_session`.

- Sys ID: `ec48b64183945b50e9c7f2d6feaad377`.
- Short description: `Request here your mentorship session!`.
- Redirecionamento: Generated task record.
- Script: apenas os comentários padrão; o preenchimento usa Map to field.

A descrição explica que o formulário facilita a solicitação e que a criação também pode ser feita na interface clássica.

| Ordem | Pergunta | Nome | Tipo | Campo de destino | Obrigatória |
|---|---|---|---|---|---|
| 100 | What's your session subject? | `short_description` | Single Line Text | Short description | Sim |
| 200 | Describe your needs for this session | `description` | Multi Line Text | Description | Não |
| 300 | When would you like to schedule your session? | `session_date` | Date/Time | Session Date | Sim |
| 400 | Choose your mentor | `mentors_name` | Reference | Mentor's Name | Sim |

Todas as variáveis usam **Map to field**. A variável de data foi corrigida de Single Line Text para Date/Time antes do teste de criação bem-sucedido.

A referência de mentor aponta para a tabela Mentor e usa o filtro simples **Available is true**. Assim, o solicitante encontra os mentores disponíveis na seleção, reaproveitando o cadastro existente.

## 2. Acesso ao produtor

Foi criado o User Criteria **Mentorship Program Users**, ativo, com os grupos:

- Mentorship Program - Mentores.
- Mentorship Program - Mentorados.

**Match All** ficou desmarcado: pertencer a qualquer um dos grupos atende ao critério. O critério foi associado à lista **Available For** do produtor. Os demais seletores não foram usados.

Essa configuração controla a disponibilidade do item; as ACLs da aplicação continuam controlando o acesso aos registros e campos.

## 3. Menu do Employee Center

Foi criado o item **New Mentorship Session** com as seguintes propriedades:

| Propriedade | Valor |
|---|---|
| Application | Mentorship Program |
| Parent Menu Item | More |
| Type | Catalog Item |
| Catalog item | Mentorship Session |
| Page | `sc_cat_item` |
| Order | 100 |
| Sys ID | `f46dfe8983945b50e9c7f2d6feaad303` |

O item **More** pertence ao **Employee Center Menu**, conforme o enunciado. O menu existente pertence à aplicação Employee Center; o novo item foi criado no escopo Mentorship Program.

Para o extra de visibilidade, o campo Condition do novo item usa a expressão:

```javascript
gs.hasRole('x_2273184_mentor_0.mentor') || gs.hasRole('x_2273184_mentor_0.mentee')
```

Essa expressão pequena verifica as roles para exibir o link. O User Criteria mantém a restrição por grupos no produtor. Esconder o link não substitui a autorização de acesso ao item.

## 4. Obrigatoriedade no formulário clássico

Foi criada a UI Policy **Obrigatoriedade dos campos da sessão**, na tabela Mentorship Session, sem condições e sem script.

- Order: 100; Active e On load marcados.
- Global marcado, aplicando a política às views do formulário. Esse campo não significa escopo Global.
- Reverse if false e Inherit desmarcados.

Foram criadas três UI Policy Actions, uma para cada campo `short_description`, `mentors_name` e `session_date`, com **Mandatory = True** e **Visible/Read only = Leave alone**.

O uso de UI Policy atende ao pedido de obrigatoriedade no formulário sem alterar a propriedade Mandatory no dicionário. No produtor, a obrigatoriedade foi definida nas próprias variáveis.

## 5. Visibilidade do feedback

Foi criada a UI Policy **Exibir feedback em sessões aceitas ou concluídas**, na tabela Mentorship Session, com Order 200, Active, Global, On load e Reverse if false marcados; Inherit desmarcado.

Condição: **State is Accepted OR State is Done**. A ação para `session_feedback` define **Visible = True**, mantendo Mandatory e Read only como Leave alone.

Com Reverse if false, o campo fica oculto quando a condição não é atendida. A política controla a apresentação; a ACL de feedback continua restringindo sua edição aos perfis autorizados.

## 6. Indicadores das fases

Foram criados cinco registros ativos em Flow Formatters (`sys_process_flow`) para Mentorship Session, no escopo da aplicação:

| Name | Label | Order | Condição |
|---|---|---|---|
| `draft` | Draft | 100 | `state=10` |
| `awaiting_approval` | Awaiting approval | 200 | `state=20` |
| `accepted` | Accepted | 300 | `state=30` |
| `done` | Done | 400 | `state=50` |
| `rejected_canceled` | Rejected/Canceled | 500 | `state=40` |

O formatter **Process flow** foi adicionado antes do campo Number no formulário clássico. Ele destaca a fase correspondente ao estado atual. As marcas nas fases anteriores são uma representação linear do componente, não uma comprovação do histórico: uma rejeição pode apresentar marcas em Accepted e Done mesmo sem passar por esses estados. O histórico real permanece nas atividades do registro.

## 7. Bloqueio de datas anteriores a hoje

Foi criada a Business Rule **Impedir data de sessão anterior a hoje.**, ativa, na tabela Mentorship Session, sem Advanced e sem script.

- Insert e Update marcados.
- Condições combinadas com AND: **Session Date before Today** e **Session Date is changed**.
- Actions: **Add message**, com `A data da sessão não pode ser anterior a hoje.`, e **Abort action**.

A validação no servidor atende tanto à criação pela plataforma quanto pelo Record Producer. A comparação é com o dia atual: horários anteriores dentro de hoje não são bloqueados por essa regra.

A condição de alteração da data evita impedir uma atualização de feedback ou de estado só porque a data de uma sessão existente já passou. O comportamento deve ser considerado com a data e o fuso utilizados no ambiente de teste.

## 8. Retorno visual da data no portal

O primeiro teste demonstrou que o servidor bloqueava a data inválida, mas o redirecionamento do produtor levava a **Record not found**, pois o registro não havia sido criado. Para orientar o usuário antes do envio, foi criada a Catalog UI Policy **Validar data da sessão no portal**.

- Catalog item: Mentorship Session; Active marcado.
- Catalog Conditions: **session_date before Today**.
- Applies on a Catalog Item view, On load e Reverse if false marcados.
- Applies on the Target Record desmarcado; sem script.

A Catalog UI Policy Action da variável `session_date`, Order 100, mantém Mandatory, Visible e Read only como Leave alone, usa **Value action = Clear value** e **Field message type = Error**, com a mensagem `A data da sessão não pode ser anterior a hoje.`.

Ao informar uma data anterior, o campo é limpo e recebe uma mensagem junto dele. Como a variável é obrigatória, o envio fica bloqueado até ser preenchida corretamente, preservando os outros valores do formulário. A mensagem deixa de ser apresentada ao corrigir a data. A Business Rule continua como validação no servidor.

## Testes confirmados

| Cenário | Evidência e resultado |
|---|---|
| Criação pelo portal como Aileen Mottern | Criada a sessão **MTS0001019**, com assunto, descrição, data e Abel Tuter como mentor; Opened by = Aileen. |
| Integração com o fluxo da Atividade 3 | A sessão passou para Awaiting approval e foi criada aprovação Requested para Abel. |
| Aprovação pelo portal | Abel encontrou a solicitação em My Tasks e aprovou; a sessão passou para Accepted. |
| Filtro de mentores | Seleção apresentou Abel, Fred e Scott; Abraham, indisponível, não apareceu. |
| Usuário sem acesso | O usuário de teste `teste` (teste da Silva), sem roles/grupos da aplicação, recebeu acesso negado pela URL do produtor; o menu ficou oculto. |
| Visibilidade do menu | Link visível para Aileen e Abel, representando os perfis mentorado e mentor. |
| Obrigatoriedade no formulário | Envio vazio do formulário não salvo MTS0001020 foi bloqueado, apontando os três campos obrigatórios. |
| Visibilidade do feedback | No formulário não salvo MTS0001021, Draft e Rejected/Canceled ocultaram o campo; Accepted e Done o exibiram. |
| Indicadores das fases | MTS0001019 destacou Awaiting approval; MTS0001017 destacou Done; MTS0001018 destacou Rejected/Canceled. |
| Data anterior na plataforma | Tentativa de criação MTS0001022 foi bloqueada com Invalid insert e a mensagem configurada. |
| Alteração para data anterior | Atualização da data da MTS0001019 foi bloqueada com Invalid update. |
| Data de hoje | Alteração da MTS0001019 para a data de hoje foi aceita; depois foi restaurada a data de 03/11/2026. |
| Data anterior no portal | Após a melhoria visual, o campo foi limpo, o erro apareceu junto da data e o envio foi impedido sem sair do produtor. Usuário confirmou o resultado. |

Os números apresentados em formulários não salvos não comprovam a existência de registros. A MTS0001019 foi observada em Accepted, com feedback ainda vazio. Não foi confirmado seu encerramento nesta etapa; não registrar novo incremento do contador por essa sessão. O contador de Abel observado anteriormente era 1, proveniente do teste concluído da Atividade 3.

## Preservação e versionamento

O usuário confirmou os commits das configurações da Atividade 4 e dos extras, incluindo a melhoria final com a mensagem **Melhora validação visual da data no portal**. Os hashes foram conferidos no GitHub em 04/11/2026:

- Record Producer, grupos e menu: `2f66b9616445d6c4d664b5a41c691f8686f43599`.
- Extras: `dbe11f71cb27956a14dc401c54eaae29a1d8d768`.
- Melhoria visual da data: `227e9bb575a97ce016c5f66c6cf3cc369946c670`.

Essa conferência confirma os commits, sem representar nova execução dos testes na PDI.

Configurações da aplicação pertencentes ao escopo são versionadas pela integração com Git. Isso não equivale a um backup completo da PDI: sessões, mentores, grupos, associações, aprovações e journals precisam de preservação separada quando não incluídos como arquivos da aplicação. Os novos dados da Atividade 4 ainda não têm exportação confirmada neste registro.

Registros Global e configurações de outros escopos exigem conferência e exportação próprias. O layout Global de Approvers já era tratado separadamente nas etapas anteriores. Arquivos Markdown e exports fora do caminho da aplicação no repositório não viram telas ou registros do ServiceNow ao executar Pull.

## Fontes e acesso

- Enunciados: `atividade 4/1 atividade 4.png`, `2 atividade 4.png`, `extra 1.png` e `extra 2.png`, na pasta do bootcamp no Desktop.
- Evidências: capturas e confirmações fornecidas durante a configuração e os testes. Este documento não representa uma nova auditoria direta da instância.
- [Employee Center](https://dev457483.service-now.com/esc).
- [Record Producer no portal](https://dev457483.service-now.com/esc?id=sc_cat_item&sys_id=ec48b64183945b50e9c7f2d6feaad377).
- [Repositório da aplicação](https://github.com/fredsons/mentorship-program).

