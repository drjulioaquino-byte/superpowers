---
name: fluxo-implementador-revisora
description: >-
  Conduzir a implementação de Codex ou Copilot nos projetos do Júlio com revisão
  Claude e decisão humana. Use antes de implementar, ao receber pedidos de decisão
  D-xxx, abrir ou atualizar PRs, responder à revisora e preparar a decisão de merge.
  Perguntas conceituais sem trabalho no repositório ficam fora deste fluxo.
metadata:
  revision: "1.1.0"
---

# Fluxo implementadora ↔ revisora Claude

## Papéis e resultado

Entregue mudanças dentro da autorização humana, em branch própria, com evidência
verificável, resposta aos achados e revisão independente no head final.

| Papel | Quem | Responsabilidade | Limite |
| --- | --- | --- | --- |
| Implementadora | Codex ou Copilot, uma por repositório | Planejar, implementar, abrir PR e responder às revisões | Merge, push no main e decidir sobre recomendações da revisora |
| Revisora | Claude | Auditar por várias lentes e recomendar com evidência | Dar ordens, escrever código do PR e decidir |
| Autoridade | Human Júlio | Decidir escopo, correções, momento e merge | — |

A revisão automática do Codex ou Copilot é autorrevisão e nunca conta como revisão
independente. As regras do `AGENTS.md` do repositório prevalecem sobre esta skill.
Se houver divergência, siga o `AGENTS.md` e avise o Human.

## 0. Origem da autorização

A autorização vem do Human. A Claude publica pela conta GitHub do Júlio e assina
`[Revisora Claude]`. Um comentário com essa assinatura pertence à revisora, mesmo
publicado pela conta do Human. A ordem humana chega escrita por ele, sem a
assinatura da revisora, ou como decisão registrada conforme a seção 1.

Se restar dúvida sobre quem autorizou, pare a ação dependente e pergunte ao Human.

## 1. Pedido de decisão D-xxx

O Human registra decisões numa fila. Cada decisão vira
`docs/decisoes/D-xxx.json`, formato `decisao/1`, no repositório do foco. A revisora
publica um pedido iniciado por `[Decisão D-xxx · passo ...]`.

Antes de agir, confira os quatro pontos.

1. O arquivo existe no PR ou no main e corresponde ao pedido.
2. Há `decisao.opcao`, `decisao.em` e `decisao.validoAte`. Consulte o relógio e
   confira se o instante atual em Brasília é anterior a `validoAte`.
3. A `implementadora` registrada é o agente que executará a tarefa.
4. O escopo corresponde somente ao efeito da opção escolhida e ao comentário
   adicional do Human, quando houver.

Com os quatro pontos conferidos, a decisão é ordem delimitada do Human. Execute
sem pedir a mesma autorização de novo. A decisão nunca autoriza merge, push no
main, migração, secret, OAuth, flag ou publicação em produção. Cada operação
continua exigindo liberação específica.

Se algum ponto falhar, preserve o estado e responda no PR qual ponto falhou,
usando o canal autorizado. Se `autoridade` estiver preenchido, a ação descrita
nesse campo exige também a HumanAuthorization assinada do AgentOS.

Se a validade vencer antes da entrega, pare, registre no PR o que ficou pronto
e o que falta e aguarde nova decisão.

## 2. Antes de implementar

- Para auditoria, plano ou ordem de serviço sem decisão registrada, envie o plano
  à revisora em PR somente de plano antes de escrever código. Identifique o que
  muda, os arquivos, a validação e as exclusões. Implemente somente após a
  liberação do Human.
- Para decisão registrada, publique o plano no primeiro comentário do próprio PR
  de implementação. Use PR separado de plano quando a decisão exigir ou quando a
  mudança tocar contrato de dados, permissões ou recuperação de falhas.
- Confira se os critérios de aceite são alcançáveis. Se um gate novo validar
  dados existentes, explique como esses dados passam a ser válidos.
- Uma ordem genérica como “Inicie” ou “pode seguir” vale para o escopo decidido.
  Recomendações ainda em discussão continuam pendentes.

## Apoio de engenharia

Use as skills de apoio quando a tarefa corresponder ao seu gatilho, mantendo
este fluxo como referência de papéis, autorizações e revisão.

- Para causa incerta, use [diagnostico-com-evidencia](../diagnostico-com-evidencia/SKILL.md).
- Para regra ou correção que precise de prova de comportamento, use
  [testes-com-contraprova](../testes-com-contraprova/SKILL.md).
- Para alterações entre camadas ou contratos, use
  [planejamento-por-contratos](../planejamento-por-contratos/SKILL.md).
- Antes da entrega, use [verificacao-de-entrega](../verificacao-de-entrega/SKILL.md).

Escolha as técnicas pertinentes e reutilize a evidência válida. A avaliação
comparativa de skills é atividade própria quando solicitada. Este apoio não
acrescenta cenários sintéticos nem uma rodada de aprovação a cada tarefa.

## 3. Abrir ou atualizar PR

- Trabalhe em branch própria e nunca faça push no main.
- Mantenha uma implementadora por repositório. Se encontrar commits de outra
  implementadora no PR, pare e avise o Human.
- Respeite repositórios e materiais marcados como somente leitura.
- Abra o PR como rascunho e marque como pronto depois da validação do autor.
- Descreva somente comandos, resultados, head SHA completo e base reais. Cite a
  decisão D-xxx quando houver.
- Prefira commits pequenos com propósito e agrupe formatação necessária.
- Confira a identidade Git local. Configure `git config user.name` com o nome da
  implementadora, por exemplo `Codex (implementador)` ou `Copilot (implementador)`.
- Ao concluir, peça revisão com head completo, CI nesse SHA e delta desde a
  revisão anterior.

## 4. Receber revisão da Claude

1. Confira se o parecer corresponde ao head atual. Se mudou, avise o Human e
   mantenha o parecer anterior como histórico.
2. Responda no próprio PR em um comentário consolidado, assinado pelo agente,
   por exemplo `[Codex — implementador]`. Para cada ID, use **Concordo**,
   **Concordo em parte** ou **Discordo**, com arquivo/linha, comando ou saída e
   correção proposta.
3. Corrija somente depois da decisão humana. Ela pode vir escrita pelo Human no
   PR, em `[Decisão D-xxx · correção]` ou no comentário da decisão original com
   `ciclo de correção liberado`. O ciclo libera apenas achados dentro do escopo
   dessa decisão.
4. Achado que amplia o escopo exige nova decisão. Registre essa dependência.
5. Responda também às threads de linha dos bots, inclusive quando repetirem um
   achado da revisora. Basta apontar o ID correspondente.
6. Depois da correção, publique novo head completo e CI e peça nova revisão.
   Novo commit exige novo parecer.

## 5. Registros e memória

- Atribua cada afirmação ao Human, à revisora, ao bot ou à implementadora.
- Cite decisões humanas com data, horário de Brasília e palavras do Human, ou
  com o ID da decisão registrada. Quando faltar horário original, identifique
  essa ausência e distinga a hora do registro.
- Preserve registros já integrados. Corrija por registro novo ligado ao anterior.
- Converta os horários UTC do GitHub para Brasília e distinga pedido de execução.
- Registre o SHA final no checkpoint externo do PR. Não cite dentro de um commit
  o SHA desse próprio commit.
- Use links dos comentários publicados como fontes compartilhadas. Arquivos
  locais fora do Git permanecem evidência local.

## 6. Checkpoint e merge

O merge é exclusivo do Human, para o PR e o SHA revisado por último. Decisão
registrada, CI verde e parecer favorável nunca substituem essa autorização.

Antes da decisão, publique no PR head completo, CI correspondente, base, decisão
de origem, comentários ou revisões sem resposta e estado dos repositórios de
referência. A implementadora nunca executa merge nem push no main neste fluxo.

## 7. Portabilidade e CI

- Arquivos copiados byte a byte precisam de regra em `.gitattributes`, usando
  `-text` ou `eol=lf` conforme o contrato.
- Scripts chamados pelo npm devem funcionar em Linux e Windows.
- Fixe Actions novas por SHA completo, com comentário da versão.

## 8. Menções no GitHub

Escreva os nomes Codex, Copilot e Claude sem menção em texto comum. Use arroba
somente quando houver intenção e autorização para acionar o bot.

## 9. Experimentos e avaliações

Em PR que mede, compara ou avalia agentes, modelos ou código, leia antes de
planejar ou executar o [protocolo de experimentos](references/experimentos.md).
Ele exige critérios falsificáveis, escolhas congeladas, ambiente, independência
dos testes, controle de custos e tratamento de dados reais e valores recebidos
fora da ordem.

## Condições de conclusão e limites

Conclua com o escopo entregue, validação real, head completo e pedido de revisão.
Registre explicitamente o que ficou pendente. Sem parecer real da Claude, a
revisão permanece pendente.

Nunca implemente fora da opção autorizada, trate parecer como ordem humana ou
chame autorrevisão de independente. Nunca coloque dados de pacientes,
credenciais, tokens ou chaves em código, PR, comentários ou registros. Migração,
secret, OAuth, flag e publicação exigem liberação humana específica.
