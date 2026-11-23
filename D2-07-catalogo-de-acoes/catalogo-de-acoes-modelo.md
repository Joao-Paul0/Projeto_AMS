# Catálogo de ações — modelo para preencher

<!--
Este arquivo é para preencher: uma linha por ação que o SEU agente vai
poder executar. As perguntas de cada coluna estão aqui em comentário.

As quatro perguntas que decidem se uma linha está boa:
  - Ação de ESCRITA também? As que alteram o mundo são as que exigem
    cuidado — e são justamente as que mais ficam de fora.
  - COMUNICAR é ação? Avisar, escalar, transferir, pedir confirmação:
    entram com entrada, saída e risco como as outras.
  - "É reversível?" pergunta se o efeito pode ser DESFEITO sem custo
    maior que o da própria ação.
  - O risco diz risco DE QUÊ — "baixo" não é descrição; "paga duas vezes
    uma nota que já estava paga" é.

Este catálogo é, literalmente, a lista de ferramentas que você vai
implementar em D10. Cada linha vira uma função com contrato.
-->

| Ação | Entrada | Saída | É reversível? | Risco se errar |
|---|---|---|---|---|
| consultar o estado da máquina | identificador da máquina e leitura atual | temperatura, vibração, horas desde manutenção e situação atual | sim — apenas lê dados; nenhuma mudança no equipamento | leitura incorreta faz o agente liberar uma máquina em risco ou interromper uma máquina saudável |
| consultar o histórico de falhas e manutenções | identificador e família da máquina, período de consulta | falhas recentes, ordens abertas e última manutenção | sim — apenas consulta o histórico | histórico incompleto oculta um padrão de falhas e pode causar nova quebra ou inspeção desnecessária |
| recomendar seguir operando | leituras atuais, histórico e regras de risco | recomendação registrada e justificativa | parcialmente — a recomendação pode ser substituída, mas o tempo operado não pode ser desfeito | falsa liberação expõe operador e equipamento a acidente, parada não planejada e custo de reparo |
| abrir ordem de inspeção | identificador da máquina, evidências e prioridade | ordem de serviço para a equipe de manutenção | parcialmente — a ordem pode ser cancelada, mas o deslocamento e o tempo da equipe podem já ter ocorrido | ordem indevida interrompe a produção e consome recursos; ordem omitida deixa uma falha sem investigação |
| parar a máquina para manutenção | identificador, motivo, evidências e confirmação do responsável | comando de parada e registro da ocorrência | parcialmente — a máquina pode voltar a operar, mas a produção perdida e o desgaste do processo não são recuperáveis | parada indevida interrompe a linha e pode danificar lotes; não parar diante de risco pode causar acidente ou dano maior |
| avisar o operador e escalar para o supervisor | destinatários, máquina, recomendação e justificativa | notificação com confirmação de recebimento e escalonamento | não — a mensagem enviada não pode ser retirada da leitura dos destinatários | alerta omitido atrasa a resposta; alerta errado provoca pânico, parada desnecessária ou ação insegura |

**Quem executa cada ação** (o agente sozinho? com confirmação humana? só
humano?): O agente pode executar sozinho as duas consultas e registrar uma
recomendação de seguir operando, desde que a justificativa e os dados usados
fiquem no registro. Ele pode abrir uma ordem de inspeção e enviar o aviso ao
operador, mas a prioridade alta e qualquer escalonamento devem ter confirmação
do supervisor. A parada da máquina exige confirmação humana do responsável pela
operação/manutenção; a execução física da manutenção é exclusiva da equipe
humana.

**O que o agente JAMAIS executa sozinho:** Parar a máquina para manutenção,
alterar parâmetros de segurança, religar equipamento parado ou autorizar a
retomada após uma falha; essas ações podem afetar pessoas, produção e a
integridade do equipamento e precisam de decisão e execução humanas.
