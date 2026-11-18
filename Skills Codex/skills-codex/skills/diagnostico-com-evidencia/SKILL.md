---
name: diagnostico-com-evidencia
description: >-
  Investigar bugs, testes intermitentes, regressões e falhas de integração cuja
  causa ainda está incerta. Use antes de propor uma correção para localizar a
  camada responsável e testar uma hipótese com evidência. Ajustes documentais
  com causa e escopo já definidos dispensam este diagnóstico.
license: MIT
metadata:
  revision: "1.0.0"
---

# Diagnóstico com evidência

Aplique junto de `fluxo-implementador-revisora` nos projetos do Júlio. Preserve
as autorizações vigentes e as regras do repositório durante a investigação.

## Investigar a causa

1. Separe o sintoma observado da causa suposta. Registre o comportamento
   esperado, a entrada, a saída e a revisão em que ocorreu. Leia a mensagem
   completa, a pilha relevante e as mudanças recentes antes de editar.
2. Reproduza pelo ponto de entrada real do componente em ambiente autorizado.
   Se a reprodução for intermitente ou indisponível, identifique essa limitação
   e reúna a evidência acessível. Evidência estática pode sustentar um achado,
   mas deve ser distinguida de execução reproduzida.
3. Siga o dado entre as camadas afetadas. Compare o contrato do chamador com o
   do chamado, os dados anteriores à falha e as condições de persistência ou
   recuperação. Reaproveite exemplos funcionais do próprio projeto.
4. Ordene as hipóteses pela evidência e pelo custo de refutá-las. Para cada
   tentativa, declare o que ela distingue. Mude uma variável por vez e explique
   o que aprendeu antes de repetir uma tentativa.
5. Proponha a menor correção na camada responsável quando o mecanismo da falha
   explicar a evidência. Se a investigação exigir ampliar o escopo autorizado,
   identifique a dependência para o Human e continue as partes independentes.

## Evidência segura e assíncrona

Use código, fixtures e metadados sanitizados. A investigação não concede acesso
a produção, dados de pacientes, credenciais ou configuração de ambiente. Em
fronteiras de componentes, observe nomes de operações, versões, contagens e
códigos de resultado. Evite registrar payloads, valores de segredos ou dados
pessoais para descobrir a causa.

Em falhas assíncronas, observe a condição relevante com limite e limpeza dos
recursos. Use relógio controlado quando ele já existir no projeto. Aumentar um
timeout sem entender a espera não resolve a hipótese. Alterações de retries,
workers e limites operacionais continuam sujeitas ao escopo da tarefa.

Tentativas que repetem o mesmo resultado sem aprendizado pedem revisão da
hipótese ou do teste. Se várias correções exigirem mudanças em camadas distintas,
examine a premissa arquitetural antes de ampliar o patch.

## Conclusão

Entregue causa e evidência, hipótese ainda aberta ou impedimento preciso. Na
correção autorizada, use `testes-com-contraprova` quando houver regressão a
proteger e `verificacao-de-entrega` para conferir o resultado.

Adaptada de [systematic-debugging](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/systematic-debugging/SKILL.md)
e [condition-based-waiting](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/systematic-debugging/condition-based-waiting.md).
Termos em [LICENSE](LICENSE).
