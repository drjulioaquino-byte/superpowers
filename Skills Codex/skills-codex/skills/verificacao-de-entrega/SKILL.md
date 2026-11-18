---
name: verificacao-de-entrega
description: >-
  Conferir uma entrega antes de declarar correção, conclusão ou prontidão para
  revisão. Use para relacionar requisitos, diff, head e resultados dos checks,
  preservando limites de evidência. Não inicia implementação ou aprovação extra.
license: MIT
metadata:
  revision: "1.0.0"
---

# Verificação de entrega

Aplique junto de `fluxo-implementador-revisora`. A conclusão precisa corresponder
ao estado que foi efetivamente examinado e validado.

## Conferir o candidato

1. Identifique repositório, branch, head e base. Confira o estado do checkout
   e o diff contra o escopo autorizado, incluindo arquivos novos e removidos.
   Preserve trabalho que pertença ao usuário ou a outra tarefa.
2. Confira cada requisito material contra a evidência que o cobre. Suíte verde
   não comprova sozinha restauração, migração aplicada, envio recebido ou uma
   camada externa que não foi exercitada.
3. Execute os checks obrigatórios do projeto e os focais pertinentes. Reaproveite
   resultados ainda válidos quando o candidato e as condições relevantes forem
   os mesmos. Repita quando alteração de código, base, ambiente ou uma falha
   nova invalidar a evidência anterior.
4. Leia o resultado final e o exit code, incluindo falhas, cancelamentos e skips.
   Mantenha a saída completa disponível quando precisar resumir logs extensos.
   Execução parcial, pendência e indisponibilidade não equivalem a sucesso.
5. Confira o CI no head candidato. Se ele executar um merge sintético, registre
   também esse SHA e a base envolvida. Após mudar o head, reavalie os checks e
   revisões que precisam ser atualizados.

## Interpretar diferenças e limites

Separe problema introduzido de falha anterior, apresentando a evidência da
comparação. Se o diff integral revelar problema fora dos trechos autorizados,
relate-o sem limpar outros arquivos por conveniência.

Para uma correção, indique a prova do comportamento esperado e a regressão
observada quando executada. A existência de um teste ou uma leitura do diff
nunca deve ser relatada como execução desse teste.

Descreva resultados como aprovado, falhou, pendente ou não executado, conforme a
evidência real. Se o projeto usar rótulos como `NOT_RUN` e `NOT_VERIFIED`, mantenha
seus significados. A revisão do autor continua sendo autorrevisão.

## Concluir e encaminhar

Atualize descrição e pedido de revisão com delta, head completo, base, checks e
limites pertinentes. Confira se os links e o estado de rascunho correspondem ao
PR atual. Encaminhe à Claude pelo canal autorizado. Registre achados e decisões
pendentes sem atribuir aprovação a uma revisão ainda não recebida.

Pare de ampliar o trabalho quando a entrega autorizada estiver verificada e
encaminhada. Integração, publicação e outras operações externas seguem a ordem
humana aplicável e os limites do fluxo implementador–revisora.

Adaptada de [verification-before-completion](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/verification-before-completion/SKILL.md).
Termos em [LICENSE](LICENSE).
