| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| largura | 16.0 | 4 | 156 | 294 | 4 | 0.0005 |
| custo_uniforme | 16.0 | 4 | 89 | 207 | 5 | 0.0002 |
| profundidade_limitada(limite=32) | 16.0 | 4 | 5 | 4 | 4 | 0.0 |
| aprofundamento_iterativo(limite=32) | 16.0 | 4 | 107 | 214 | 4 | 0.0003 |

**conclusão**

Não, nesta tabela, as quatro buscas acharam o mesmo custo (16.0) com 4 ações, então nenhuma foi mais barata que a largura.
O custo uniforme só se saiu melhor em esforço, expandiu 89 nós contra 156 da largura. Os custos dos caminhos são parecidos, então o caminho mais raso também é o mais barato.
