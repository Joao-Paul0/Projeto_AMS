| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| largura | 20.0 | 5 | 2786 | 6744 | 5 | 0.0061 |
| custo_uniforme | 10.0 | 6 | 1447 | 3587 | 8 | 0.0038 |
| profundidade_limitada(limite=32) | 20.0 | 5 | 6 | 5 | 5 | 0.0 |
| aprofundamento_iterativo(limite=32) | 20.0 | 5 | 1192 | 3749 | 5 | 0.0044 |
| gulosa[admissivel] | 14.0 | 4 | 5 | 22 | 4 | 0.0001 |
| a_estrela[admissivel] | 14.0 | 4 | 30 | 77 | 4 | 0.0003 |
| gulosa[inadmissivel] | 38.0 | 7 | 8 | 28 | 7 | 0.0002 |
| a_estrela[inadmissivel] | 24.0 | 5 | 6 | 25 | 5 | 0.0001 |

## conclusão

A heurística admissível é melhor porque não superestima o custo até o objetivo, permitindo que o A* encontre o caminho ótimo (14.0 com 4 ações). Já a inadmissível pode superestimar esse custo e levar a caminhos piores, como aconteceu com o A* (24.0) e a busca gulosa (38.0). Apesar de ser mais rápida, pois o A* inadmissível expandiu apenas 6 nós contra 30 da admissível, acaba sacrificando a qualidade da solução.

