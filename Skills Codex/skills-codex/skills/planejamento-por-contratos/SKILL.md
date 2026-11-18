---
name: planejamento-por-contratos
description: >-
  Planejar alterações que atravessam módulos, dados, APIs, permissões,
  persistência ou recuperação. Use para verificar se os critérios de aceite
  cabem nos contratos reais e definir incrementos verificáveis. Edições pequenas
  com requisitos completos seguem diretamente o escopo já autorizado.
license: MIT
metadata:
  revision: "1.0.0"
---

# Planejamento por contratos

Aplique junto de `fluxo-implementador-revisora`. O plano descreve o caminho para
cumprir a decisão humana e conserva os gates de revisão previstos pelo projeto.

## Conferir as premissas

Leia a ordem, os registros aplicáveis e os arquivos que já implementam o
comportamento. Identifique repositório, base, estado local, escopo e dependências.
Procure funções, representações, fixtures e fluxos reutilizáveis antes de criar
outra infraestrutura.

Mapeie somente as camadas afetadas. Para cada interface importante, confira
entrada, saída, identidade, autoridade e comportamento em falha. Use o contrato
que o código ou a fonte canônica realmente impõe. Um nome semelhante ou uma
suposição sobre o serviço não comprova compatibilidade.

Quando houver persistência, examine também o estado já existente, atomicidade,
concorrência, reentrega e restauração pertinentes. Se um gate novo exigir dados
em outro formato, explique como os registros anteriores passam a satisfazê-lo.
Uma migração necessária entra como dependência com autorização própria.

## Tornar o aceite alcançável

Ligue cada requisito material ao resultado esperado, à camada responsável e à
evidência prevista. Confira os conflitos entre critérios antes de escrever
código. Por exemplo, guardar nome e telefone num cadastro restaurável precisa
ser compatível com a política dos snapshots e com a minimização de auditoria.

Distinga observação local, simulação e operação externa. Indique qual evidência
falta quando um teste não alcança a camada do requisito. Planos de integração
devem declarar qual sistema mantém a identidade e o que ocorre numa resposta
perdida, numa repetição ou numa alteração concorrente relevante.

## Delimitar a implementação

- Defina os arquivos e responsabilidades que a autorização permite alterar.
  Preserve interfaces existentes e evite refatoração paralela.
- Divida trabalho complexo em incrementos que tenham comportamento verificável.
  Explicite os nomes, tipos e valores que uma tarefa consome de outra quando
  eles forem necessários para evitar incompatibilidade.
- Compare alternativas quando houver uma escolha real com custos ou riscos
  distintos. Resolva detalhes rotineiros já cobertos pela ordem sem pedir nova
  autorização. Escolhas de produto ou ampliação de escopo voltam ao Human.
- Declare comandos de validação, riscos pertinentes e condições de conclusão.
  Identifique rollback ou recuperação quando a mudança os exigir.
- Faça a autoconferência contra os requisitos e os contratos observados. Ajuste
  somente o plano dentro do escopo. A revisão da Claude segue o fluxo vigente.

## Conclusão

Entregue um plano no local exigido pelo projeto, com premissas verificadas,
dependências explícitas e critérios executáveis. Em trabalhos longos, registre
último head validado, decisões e próxima ação para permitir retomada sem refazer
etapas. Preserve a distinção entre plano preparado, revisado e autorizado.

Adaptada de [writing-plans](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/writing-plans/SKILL.md).
Termos em [LICENSE](LICENSE).
