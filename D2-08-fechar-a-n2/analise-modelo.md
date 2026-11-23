# Análise — uma página

## O que torna o problema difícil

O ambiente é parcialmente observável, estocástico, sequencial e dinâmico. A
linha de base vê as leituras atuais e as falhas já reveladas, mas não observa
todas as condições da máquina nem conhece o futuro. Isso aparece nos casos
C07 e C08: a regra liberou a operação, embora o rótulo correto fosse
`inspecionar_antes_de_operar`. Nos casos C11 e C22 ocorreu o inverso: o agente
mandou parar quando a decisão correta era inspecionar. Portanto, os mesmos
limiares de temperatura e vibração não distinguem com segurança todos os
níveis de risco. O C10 mostra outra dificuldade: o histórico recente do TORNO
pesou demais e produziu uma inspeção desnecessária. A janela temporal e a
ordem dos casos importam, porque cada desfecho observado altera as decisões
seguintes.

Há também um espaço de estados com ações de custos diferentes. No subproblema
`diagnostico:MAIOR`, a busca em largura e o custo uniforme chegaram a custo
16, mas expandiram, respectivamente, 156 e 89 nós; logo, o custo das ações e
a ordem de investigação mudam o esforço da solução. A heurística declarada
admissível levou o A* a expandir 30 nós, 59 a menos que o custo uniforme, mas a
execução encontrou custo 14 contra 16 do custo uniforme. Essa divergência é
uma evidência de que a formulação, a contagem ou a implementação precisa ser
verificada antes de afirmar a optimalidade. A profundidade limitada também
não é diretamente comparável: seus 5 nós são entradas recursivas, sem a
mesma contagem de fronteira das outras buscas.

## Que tipo de agente o problema realmente exige

Um agente reativo simples não basta. Ele pode usar os limiares do registro
atual para interromper uma máquina em risco evidente, mas não consegue
representar as falhas anteriores, a data de cada observação e a janela de
falhas recentes. O tipo mínimo adequado é um agente baseado em modelo, com
estado interno que registre pelo menos a família da máquina, os desfechos
observados e sua recência; a linha de base já usa uma janela de sete dias.
Esse estado é necessário para um ambiente parcial e sequencial, mas não deve
ser confundido com conhecimento do futuro: o desfecho só entra na memória
depois que o ambiente o revela.

Para a parte de diagnóstico, o agente também precisa ser orientado a
objetivos e usar busca: o objetivo é concluir as verificações essenciais, e o
custo representa o tempo ou o esforço das ações. A heurística pode reduzir a
exploração, desde que seja validada contra o modelo de transição e os custos.
Um agente com aprendizagem pode ser acrescentado depois para calibrar risco e
limiares, mas não substitui o estado interno, a função de objetivo, os custos
nem a supervisão humana. A escolha dispensa autonomia irrestrita: o sistema
deve recomendar, justificar e encaminhar casos críticos ao técnico ou
supervisor.

## O que isto muda no projeto (fecho)

Na D10, o agente deve combinar as regras rápidas com mais histórico por
máquina, leituras adicionais e um modelo que estime a incerteza, além de um
verificador externo para validar decisões críticas. A linha de base continua
competitiva nos casos simples — acertou 25 de 30 — porque é barata, rápida e
auditável. Seus cinco erros não são um fracasso: mostram exatamente onde o
novo agente precisa melhorar, sobretudo na fronteira entre liberar, inspecionar
e parar, mantendo a decisão final com o responsável humano.
