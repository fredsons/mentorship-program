# Grupos da Atividade 2 — Brazil

Exportações manuais fornecidas em 30/10/2026, PDI dev457483. Cópias preservadas sem modificar o conteúdo dos XMLs.

| Arquivo | Registros |
|---|---:|
| mentorship-groups.xml | 2 grupos |
| mentorship-group-roles.xml | 2 atribuições de role |
| mentorship-group-members.xml | 5 membros |

- Mentores: `.mentor`, Inherits true; Scott Seixas, Fred Luddy e Abel Tuter.
- Mentorados: `.mentee`, Inherits true; Aileen Mottern e Adela Cervantsz.

Todos os vínculos de grupo foram conferidos por sys_id contra os dois grupos exportados. As roles referenciadas correspondem às roles dos XMLs de ACLs revisados. Os usuários não estão incluídos nestes arquivos; são referências a registros existentes da PDI. Scott e Fred possuem admin global e não são os usuários de validação das restrições.

Em uma recuperação, instalar primeiro a aplicação com as roles; conferir a existência e os sys_ids dos usuários; importar os grupos e depois seus vínculos de roles e membros. Verificar a propagação das roles e repetir os testes com usuários sem admin. Não importar cópias de roles herdadas por usuário como substituto da associação aos grupos.

Esta exportação não é backup integral da PDI. Restauração não testada. Preservação local confirmada; publicação no GitHub ainda pendente.
