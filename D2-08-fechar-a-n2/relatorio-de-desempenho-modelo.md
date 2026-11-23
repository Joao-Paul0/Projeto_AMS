# Relatório de desempenho da linha de base

**Projeto:** AMS — Assistente de Manutenção Segura · **Data:** 01/11/2026

## 1. A métrica primária

A métrica primária é o **acerto da decisão**: número de casos em que a ação
decidida pelo agente é igual à ação correta rotulada, dividido pelo total de
casos avaliados. Assim, `acerto = acertos / total`.

## 2. O valor

Resultado reproduzido com `D2-06-agente-baseline/medir.py`:

**25/30 = 0,8333** (83,33%).

## 3. O conjunto

Foi usado o conjunto de reserva `D2-06-agente-baseline/casos-de-reserva.csv`,
com 30 casos rotulados de manutenção industrial. Os casos foram processados
em ordem cronológica, atualizando o estado interno do agente após cada
desfecho. A distribuição dos rótulos é: 16 `seguir_operando`, 7
`parar_para_manutencao` e 7 `inspecionar_antes_de_operar`.

O conjunto foi inventado pela coordenação do curso para fins didáticos em
30/08/2026; não é uma base pública nem representa dados reais de uma empresa.

## 4. Onde o agente erra

Os cinco erros impressos pelo `medir.py` foram:

- C07: decidiu `seguir_operando`; o correto era `inspecionar_antes_de_operar`.
- C08: decidiu `seguir_operando`; o correto era `inspecionar_antes_de_operar`.
- C10: decidiu `inspecionar_antes_de_operar`; o correto era `seguir_operando`.
- C11: decidiu `parar_para_manutencao`; o correto era `inspecionar_antes_de_operar`.
- C22: decidiu `parar_para_manutencao`; o correto era `inspecionar_antes_de_operar`.

O padrão principal é a dificuldade em calibrar decisões intermediárias de
risco: quatro erros (C07, C08, C11 e C22) envolvem o rótulo
`inspecionar_antes_de_operar`. Nos dois primeiros, o agente subestima o risco
e libera a operação; nos dois últimos, superestima o risco e manda parar. O
erro C10 ocorre no sentido oposto ao dos casos C07 e C08: o agente inspeciona
quando deveria seguir operando.

A hipótese é que as regras fixas da linha de base generalizam demais os
limiares e não combinam adequadamente os sinais atuais com o histórico por
tipo de máquina. O estado interno ajuda, mas não representa todo o contexto
necessário para distinguir risco baixo, intermediário e alto. Em particular,
o histórico de falhas anteriores do TORNO parece pesar demais no C10, enquanto
os sinais dos casos C07, C08, C11 e C22 não são suficientes, para essas
regras, para escolher a ação intermediária correta.

## 5. A tabela comparativa de busca (item 4 da N2)

Resultados reproduzidos para `problemas.diagnostico:MAIOR`, com limite 32:

| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| largura | 16.0 | 4 | 156 | 294 | 4 | 0.0007 |
| custo_uniforme | 16.0 | 4 | 89 | 207 | 5 | 0.0004 |
| profundidade_limitada(limite=32) | 16.0 | 4 | 5 | 4 | 4 | 0.0 |
| aprofundamento_iterativo(limite=32) | 16.0 | 4 | 107 | 214 | 4 | 0.0005 |
| gulosa[admissivel] | 14.0 | 4 | 5 | 22 | 4 | 0.0001 |
| a_estrela[admissivel] | 14.0 | 4 | 30 | 77 | 4 | 0.0004 |
| gulosa[inadmissivel] | 38.0 | 7 | 8 | 28 | 7 | 0.0002 |
| a_estrela[inadmissivel] | 24.0 | 5 | 6 | 25 | 5 | 0.0001 |

Na execução reproduzida, o A* com a heurística declarada admissível expandiu
30 nós, contra 89 do custo uniforme: economizou **59 nós**, ou cerca de
**66,3%**. Porém, não manteve o mesmo custo de referência: encontrou custo
14, enquanto o custo uniforme encontrou custo 16. Portanto, os números não
permitem afirmar simultaneamente que o custo 16 é ótimo e que a heurística é
admissível; há uma inconsistência que deve ser verificada na implementação,
na contagem ou na comparação da formulação antes de atribuir ao A* uma
garantia de optimalidade. Ainda assim, a redução de expansões mostra que a
heurística direciona a busca para uma região muito menor do espaço de estados.

Na profundidade limitada, a contagem tem uma ressalva importante: a busca é
recursiva e não possui fronteira; `nós expandidos` conta entradas na recursão,
sem repetidos. Por isso, a vantagem aparente de 5 expansões não é diretamente
comparável à contagem das buscas que usam fronteira.
