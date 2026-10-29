# Layout Global de Approvers — arquivos exportados

`approvers-layout-global.xml` contém o registro **sys_ui_list** do layout. Seus elementos estão exportados separadamente em `approvers-layout-elements.xml`.

- Instância de origem: dev457483 (Brazil).
- sys_id do layout: `6cc0b26883185750e9c7f2d6feaad330`.
- Tabela: sysapproval_approver.
- Parent: x_2273184_mentor_0_mentorship_session.
- View: Default view.
- Escopo: Global.
- Data de exportação informada no XML: 2026-10-29 21:53:57 (horário do arquivo, sem conversão).

Recebido e validado também `approvers-layout-elements.xml`, exportado em 2026-10-29 21:56:30 (horário informado no XML). Contém exatamente três registros sys_ui_list_element: state (posição 0), approver (1) e comments (2). Todos referenciam o sys_id do layout acima. Os dois arquivos foram preservados sem alteração de conteúdo.

O conjunto contém o registro de layout e seus três elementos. Foi verificada a estrutura XML e a associação entre registros; nenhum teste de importação/restauração foi executado. Para recuperar em outra instância, restaurar primeiro a aplicação e conferir possíveis layouts existentes nesse mesmo contexto; depois considerar o registro de layout e seus elementos em conjunto. Essas exportações não representam backup dos registros de aprovação nem da PDI inteira.

Estes arquivos são complementares à aplicação scoped. Incluí-los no repositório não os importa automaticamente para o ServiceNow.
