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

## Próxima etapa

A Atividade 2 tratará roles, grupos, ACLs e restrições de menus. As permissões atuais são provisórias da Atividade 1. Fluxo automático de aprovação e atualização automática do contador ainda não foram implementados.
