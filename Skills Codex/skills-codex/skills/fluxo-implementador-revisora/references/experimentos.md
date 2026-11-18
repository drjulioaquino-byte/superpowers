# Protocolo para experimentos e avaliações

Aprendizado fornecido pelo Human a partir do GEM, novembro de 2026. Aplicar a todo
PR que mede, compara ou avalia agentes, modelos ou código.

1. **Plano que pode falhar.** Antes de propor, confira se os braços são de fato
   diferentes, se o gabarito não é seu e se o critério é alcançável nos dois
   sentidos. Inclua estimativa de desenvolvimento quando o desfecho for incerto.
2. **Congelar antes do teste.** Fixe por commit as partições, hiperparâmetros
   candidatos, desempates, métrica e critério. Sele as escolhas e os pesos antes
   de ler a primeira partição de teste. Declare as sementes de desenvolvimento.
3. **Registrar o ambiente.** Grave no relatório Python, NumPy, backend numérico e
   variáveis de thread. Rode com uma thread quando o plano pedir e guarde a
   invocação exata.
4. **Saída portável.** Arredonde valores antes do uso e do hash quando o resultado
   precisar coincidir entre máquinas. Declare quais valores coincidem byte a byte
   e quais dependem do ambiente.
5. **Teste que falha antes da correção.** Toda correção vem com teste sintético
   que falha no código antigo, cobrindo todas as partições e regimes afetados,
   além do caso que revelou o defeito.
6. **Gerador de teste independente.** Os dados de teste não podem compartilhar
   componentes ou premissas com o método testado. Registre as dependências antes
   de pontuar.
7. **Dados reais.** Nunca declare dados como fictícios sem varredura. Se encontrar
   dado real, como laudo, documento ou nome, pare e relate somente caminhos,
   blobs, commits e contagens. Corrija o scanner com teste sintético.
8. **Gastos.** Em protocolos com chamadas pagas, registre teto, reserva antes de
   cada tentativa, tentativas sem resposta e custo efetivo, com cadeia de recibos.
9. **Valor fora de ordem.** Um sal, chave ou segredo recebido antes da hora prevista
   não é usado. Avise e espere um novo.
10. **Hipótese não vira regra.** Transferências de
    `docs/metodologia/aprendizados-2026-11.md` são **HIPÓTESE (NOT_VERIFIED)**.
    Para testar uma, faça pré-registro próprio com decisão do Human. Esse caminho
    pertence ao projeto de origem. Se faltar no repositório em análise, solicite
    a referência antes de usar uma transferência específica.
