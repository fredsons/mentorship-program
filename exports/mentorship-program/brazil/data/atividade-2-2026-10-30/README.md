# Dados de teste da Atividade 2 — 30/10/2026

PDI dev457483, Brazil, escopo x_2273184_mentor_0. Exportações manuais fornecidas pelo usuário, preservadas sem alteração do conteúdo. A cópia histórica da Atividade 1 permanece no diretório superior.

| Arquivo | Conteúdo |
|---|---|
| mentors-data.xml | 4 mentores: Abel, Abraham, Scott e Fred |
| mentorship-sessions-data.xml | 2 sessões e 3 registros sys_journal_field incorporados |
| mentorship-session-journals.xml | Os mesmos 3 registros sys_journal_field, exportados separadamente |

## Conferência

- Todos os mentors_name das sessões apontam para um dos quatro mentores exportados.
- Todos os element_id dos journals apontam para uma das duas sessões exportadas.
- Os três journals têm os mesmos sys_ids e valores no XML das sessões e no XML separado. Eles são cópias dos mesmos registros, não seis entradas distintas.
- MTS0001009: criada por admin, mentor Abel, com a nota inicial de acompanhamento.
- MTS0001015: criada por aileen.mottern, mentor Abel; Description termina em atualizado2, feedback preservado como Feedback de teste do mentor Abel.; contém comentário inicial e nota de trabalho publicados por Aileen.
- O mentor temporário MEN0001013 não está presente, coerente com o teste de exclusão.

## Recuperação

Instalar a aplicação a partir do commit de configuração antes de importar dados. Conferir os usuários referenciados e seus sys_ids; os cadastros sys_user não estão incluídos. Importar mentores antes das sessões. O XML de sessões já inclui as três entradas de journal; o arquivo separado serve como cópia complementar e para recuperação seletiva, não como exigência de uma segunda importação. Caso seja usado, manter os sys_ids e conferir que não foram produzidas entradas duplicadas.

Não inclui histórico completo de auditoria nem restauração integral da PDI. A restauração não foi executada. O source control não importa automaticamente estes arquivos, pois estão fora da pasta nativa da aplicação.
