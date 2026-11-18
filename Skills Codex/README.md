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
| [diagnostico-com-evidencia](skills-codex/skills/diagnostico-com-evidencia/SKILL.md) | Investigar causas incertas antes da correção |
| [testes-com-contraprova](skills-codex/skills/testes-com-contraprova/SKILL.md) | Proteger comportamento com testes que detectam a falha relevante |
| [planejamento-por-contratos](skills-codex/skills/planejamento-por-contratos/SKILL.md) | Conferir critérios de aceite e interfaces entre camadas |
| [verificacao-de-entrega](skills-codex/skills/verificacao-de-entrega/SKILL.md) | Relacionar requisitos, head, diff e evidências da entrega |

O protocolo de experimentos está na
[referência da skill](skills-codex/skills/fluxo-implementador-revisora/references/experimentos.md).
O pacote `0.2.0` contém o fluxo principal na revisão `1.1.0` e quatro skills de
apoio na revisão `1.0.0`. Elas aproveitam técnicas do Superpowers e preservam o
fluxo de autorização do Júlio. Origem e atribuição estão em
[NOTICE.md](skills-codex/NOTICE.md). Os arquivos usam finais de linha LF.

## Validação

Conferir o frontmatter das skills, os links relativos, as licenças e a consistência
dos dois manifestos. As cópias pessoais instaladas devem corresponder aos arquivos
versionados. Júlio dispensou cenários sintéticos de avaliação das skills em
17/11/2026. A validação de formato e instalação é distinta de um teste de
carregamento do pacote completo como plugin no cliente.
