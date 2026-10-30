# Dados da Atividade 3 — 30/10/2026

Arquivos originais fornecidos pelo usuário, copiados sem modificar os XMLs. Marco complementar da entrega da Atividade 3.

- mentors-data.xml: 4 mentores; Abel com Concluded Sessions = 1, demais com 0.
- mentorship-sessions-data.xml: 4 sessões e 7 registros sys_journal_field incorporados.
- MTS0001009: Draft (10); MTS0001015: Accepted (30), marcos anteriores.
- MTS0001017: Done (50), approval=approved, feedback HTML completo.
- MTS0001018: Rejected/Canceled (40), approval=rejected, feedback vazio.

- approvals-data.xml: 2 registros sysapproval_approver; approved para MTS0001017 e rejected para MTS0001018, ambos com aprovador Abel Tuter. Inclui 1 sys_journal_field com a justificativa da rejeição, vinculado à aprovação rejeitada.

Referências das sessões aos mentores, das aprovações às sessões e dos journals aos respectivos registros conferidas. O XML de sessões inclui o histórico textual de aprovação/rejeição; os registros de aprovação estão no XML complementar. Não é necessário exportar novamente os mesmos journals em arquivo separado. São 8 journals distintos no conjunto dos dois XMLs.

Os dados não são importados automaticamente por Pull from repository. Em restauração, conferir usuários referenciados, importar primeiro a configuração e os mentores, depois as sessões e suas aprovações. Fluxos ativos podem reagir à criação de registros; planejar a restauração antes de importar. Restauração em outra PDI ainda não testada. O arquivo não representa o histórico completo de auditoria nem as execuções do fluxo.
