# Skills Codex

Coleção pessoal do Júlio, mantida no fork `drjulioaquino-byte/superpowers`.
O pacote `skills-codex` agrupa os fluxos próprios usados com Codex e revisão
Claude.

## Pacote

O diretório do plugin é `Skills Codex/skills-codex`. Ele contém o manifesto
portável `plugin.json` e o manifesto de compatibilidade Codex em
`.codex-plugin/plugin.json`. Ambos apontam para o mesmo pacote e versão.

| Skill | Finalidade |
| --- | --- |
| [fluxo-implementador-revisora](skills-codex/skills/fluxo-implementador-revisora/SKILL.md) | Implementação por Codex ou Copilot, revisão Claude e decisões do Human |

O protocolo de experimentos está na
[referência da skill](skills-codex/skills/fluxo-implementador-revisora/references/experimentos.md).
As instruções da skill e seus metadados foram copiados da versão pessoal
`1.0.0`, preservando o conteúdo e usando finais de linha LF no Git.

## Validação

Conferir o frontmatter da skill, seus links relativos, a consistência dos dois
manifestos e a igualdade de conteúdo com a origem pessoal após normalizar os
finais de linha para LF. O
carregamento deste pacote como plugin deve ser conferido em sessão própria do
cliente antes de declarar a integração validada.
