---
name: testes-com-contraprova
description: >-
  Criar ou revisar testes de comportamento que protegem uma correção, regra nova
  ou contrato de integração. Use para demonstrar qual falha concreta cada teste
  detecta e evitar expectativas derivadas da própria implementação. Documentação
  e criação de skills não exigem cenários sintéticos por este procedimento.
license: MIT
metadata:
  revision: "1.0.0"
---

# Testes com contraprova

Aplique junto de `fluxo-implementador-revisora` e dos checks exigidos pelo
projeto. Escolha provas proporcionais ao comportamento alterado.

## Definir a prova

Antes de escrever um teste novo, diga qual comportamento incorreto deve fazê-lo
falhar e qual resultado observável distingue o correto. Reutilize a cobertura
existente quando ela já comprovar esse ponto. Uma mudança apenas documental ou
sem regressão relevante não ganha testes que repetem sua redação.

Derive as expectativas dos requisitos, de valores conferidos ou de uma fonte
canônica. Calcular o esperado com a função testada ou seus mesmos auxiliares
pode repetir o defeito dos dois lados da asserção.

## Executar e interpretar

1. Para uma regressão, faça o teste falhar no código defeituoso quando for
   viável. Para comportamento novo, observe a ausência que ele deve detectar.
   Diferencie falha da asserção esperada, erro de setup e recurso indisponível.
2. Exercite o ponto de entrada e a camada responsáveis pela regra. Em uma
   integração, um handler com armazenamento em memória não comprova restrições
   de RPC, atomicidade real ou entrega externa. Preserve essa distinção na
   evidência e teste a fronteira pertinente quando autorizada.
3. Aplique a correção autorizada e confira o resultado. Se for útil avaliar
   uma guarda específica, use uma mutação isolada em cópia descartável e exija
   falha pelo motivo previsto. Preserve o checkout e as alterações do usuário.
4. Verifique o estado final e os efeitos, além do status ou exit code. Um
   erro de orçamento pode ser informado mesmo após uma escrita indevida.
   Deduplicar o mesmo evento e excluir ciclos distintos também são contratos
   diferentes e precisam de observações que os distingam.
5. Rode o teste focal e os checks obrigatórios pertinentes. Amplie a validação
   quando houver evidência de impacto adicional. Preserve falhas, skips e
   cancelamentos no relatório, em vez de tratá-los como aprovação.

## Dublês e concorrência

Use o código real na lógica sob avaliação. Quando a dependência externa exigir
substituição, mantenha o contrato relevante e confira efeitos do componente,
incluindo rejeições. Uma simulação permissiva não comprova a regra do serviço
real. Nunca use pacientes, credenciais ou serviços reais como atalho de teste.

Para concorrência, verifique a identidade das operações, o número de gravações
e a preservação do estado. Garanta que esperas terminem e recursos sejam
liberados também na falha. Cancelar testes seguintes não substitui uma asserção
explícita sobre a operação incorreta.

## Conclusão

Relate a falha protegida, os comandos executados e o resultado antes e depois
quando disponível. Se a contraprova não pôde ser executada, declare esse limite.
Não enfraqueça asserções, mude workers ou aumente timeouts para obter verde.

Adaptada de [test-driven-development](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/test-driven-development/SKILL.md)
e [writing-good-tests](https://github.com/drjulioaquino-byte/superpowers/blob/22f0b463e7a5e579904dd6211a520321035526f7/skills/test-driven-development/writing-good-tests.md).
Termos em [LICENSE](LICENSE).
