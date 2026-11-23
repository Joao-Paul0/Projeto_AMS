| Busca | Custo | Ações | Nós expandidos | Nós gerados | Prof. máx. | Segundos |
|---|---:|---:|---:|---:|---:|---:|
| largura | 20.0 | 5 | 2786 | 6744 | 5 | 0.0061 |
| custo_uniforme | 10.0 | 6 | 1447 | 3587 | 8 | 0.0038 |
| profundidade_limitada(limite=32) | 20.0 | 5 | 6 | 5 | 5 | 0.0 |
| aprofundamento_iterativo(limite=32) | 20.0 | 5 | 1192 | 3749 | 5 | 0.0044 |

**conclusão**

Sim, a busca de custo uniforme achou um caminho mais barato que a largura neste subproblema. O custo caiu de 20.0 (largura) para 10.0 (custo uniforme), ou seja, metade. Isso mostra que os custos das ações aqui não são parecidos existem ações caras e baratas e é isso que dá vantagem ao custo uniforme. 

