# Mentorship Program — Shark Academy

Aplicação ServiceNow para cadastrar mentores e acompanhar sessões de mentoria, desenvolvida durante o bootcamp Shark Academy.

**Atividade 1 concluída em 29/10/2026 na versão Brazil.** A aplicação foi reconstruída na PDI dev457483 após a indisponibilidade da implementação original em Zurich.

| Componente | Identificação |
|---|---|
| Escopo | `x_2273184_mentor_0` |
| Aplicação | `540f96e483945750e9c7f2d6feaad334` |
| Mentor | `x_2273184_mentor_0_mentor` |
| Mentorship Session | `x_2273184_mentor_0_mentorship_session`, extensão de Task |
| Branch | `main` |

## Conteúdo

- O diretório `540f96e483945750e9c7f2d6feaad334/` contém os arquivos gerados pelo Source control do ServiceNow.
- [Documentação da Atividade 2](https://github.com/fredsons/mentorship-program/blob/main/docs/ATIVIDADE-2-BRAZIL.md): roles, grupos, ACLs, menus, testes e limites da validação.
- [Documentação da Atividade 1](https://github.com/fredsons/mentorship-program/blob/main/docs/ATIVIDADE-1-BRAZIL.md): etapas, decisões e validações.
- [Exportações complementares](https://github.com/fredsons/mentorship-program/tree/main/exports/mentorship-program/brazil): dados de teste e layout Global de Approvers.

## Funcionalidades entregues

- Cadastro de mentores com especialidade, disponibilidade e contador inicial de sessões concluídas.
- Sessões com mentor, data/hora, feedback HTML e histórico de atividades.
- Estados Draft, Awaiting approval, Accepted, Rejected/Canceled e Done.
- Seleção restrita a mentores disponíveis.
- Sessões relacionadas no cadastro do mentor e aprovadores relacionados na sessão.
- Menu com criação e consulta das duas tabelas.

## Preservação e recuperação

O Source control guarda a configuração da aplicação. Os XMLs em `exports/` são complementares e **não são importados automaticamente** ao vincular o repositório.

Para recuperar, instalar/importar primeiro a aplicação; conferir os usuários referenciados; restaurar os mentores antes das sessões; e tratar separadamente o layout Global e seus elementos. Consultar os READMEs das exportações. O teste em outra instância ainda não foi executado.

Alterações feitas pelo ServiceNow precisam de novos commits. Após alterações feitas diretamente no GitHub, sincronizar pelo menu **Source control → Pull from repository** antes de continuar o desenvolvimento. Havendo mudanças locais, preservá-las antes de atualizar; não descartá-las para resolver conflitos.

## Atividade 2 — estado atual

Configurações de segurança enviadas pelo ServiceNow no commit `7d33fb0f2c064f94daf6445b34b8fc5134096c7b`: roles mentor/mentee, 19 ACLs ativas e menus por perfil. As roles e ACLs provisórias da Atividade 1 foram removidas. Os testes observados e os cenários ainda pendentes estão na documentação da Atividade 2; a documentação distingue os resultados observados dos testes por API e de restauração, que não foram executados.

Exportações complementares da Atividade 2 preservam dois grupos, duas atribuições de roles, cinco membros, quatro mentores, duas sessões e três journals. Os usuários referenciados não estão incluídos. O XML de sessões já inclui as mesmas notas do arquivo de journals separado.

A Atividade 2 tratou da segurança. A automação de aprovação e do contador foi implementada na Atividade 3, descrita abaixo.

## Atividade 3 — fluxo e testes validados em 30/10/2026

[Documentação da Atividade 3](docs/ATIVIDADE-3-BRAZIL.md): fluxo ativo como System User, aprovação pelo mentor, espera por feedback, conclusão e incremento via FX Add. Caminhos de aprovação e rejeição validados; Session Feedback ampliado para 4000 caracteres, mantendo HTML. Configuração preservada no commit `40346b001294a112f3b2dbfbe4cfc009a2a4a268`. Exportações atuais preservadas em [atividade-3-2026-10-30](exports/mentorship-program/brazil/data/atividade-3-2026-10-30/): 4 mentores, 4 sessões, 2 aprovações e 8 journals incorporados. Vínculos e estados conferidos; os XMLs da Atividade 2 permanecem históricos. Restauração em outra PDI não testada.
