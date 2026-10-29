# Dados de teste — Mentorship Program / Brazil

Origem: dev457483. Arquivos fornecidos pelo usuário em 29/10/2026, preservados sem alteração do conteúdo original.

## Inventário validado

| Arquivo | Registros |
|---|---|
| mentors-data.xml | 2 mentores |
| mentorship-sessions-data.xml | 1 sessão e 1 registro sys_journal_field de Work notes |

- Abel Tuter, MEN0001006: available=true, expertise_area=it, concluded_sessions=0. sys_id: `1e7daae083185750e9c7f2d6feaad339`.
- Abraham Lincoln, MEN0001007: available=false, expertise_area=financial, concluded_sessions=0. sys_id: `d83936e883585750e9c7f2d6feaad32e`.
- Sessão MTS0001009: sys_id `945ea26483185750e9c7f2d6feaad3f7`, state=10 (Draft), mentors_name apontando para Abel Tuter.
- Nota de trabalho: “Primeiro registro de acompanhamento.”, associada à mesma sessão via element_id.

As referências sessão→mentor e nota→sessão foram verificadas nos XMLs. A exportação de dados também confirma a existência do mentor indisponível que não apareceu na captura da lupa.

## Recuperação e limites

Restaurar primeiro a estrutura da aplicação e conferir suas dependências. Os mentores referenciam usuários sys_user e a sessão referencia o usuário de abertura; os registros completos desses usuários não estão incluídos. Validar a existência ou mapear essas referências na instância de destino.

Importar os mentores antes das sessões. A exportação de sessão inclui sua nota de trabalho, mas não deve ser considerada uma cópia completa do histórico de auditoria ou de todas as tabelas relacionadas. Não contém registros de aprovadores, que estavam ausentes no teste.

A validação foi estrutural e de integridade das referências internas; não foi executado teste de importação/restauração. Datas foram mantidas conforme os arquivos, sem conversão. A inclusão destes arquivos no repositório não os importa automaticamente para o ServiceNow.
