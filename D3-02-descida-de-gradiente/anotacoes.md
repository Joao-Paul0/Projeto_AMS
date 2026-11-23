# Anotações — Laboratório 02, a descida à mão

> O critério do slide 11: as quatro perguntas respondidas por escrito, com o
> número que sustenta cada resposta. Preencha a tabela rodando o esqueleto
> com as três taxas do slide 12 e copiando a última linha de cada execução.

## A última linha de cada taxa

| Taxa | Última linha da saída (perda, w, b) |
|---|---|
| 0,001 | `passo  200 perda 22462.1 w 215.016 b -17.7381` |
| 0,1 | `passo  200 perda 0.752176 w 300.008 b 4.91185` |
| 1,5 | `passo  200 perda inf w -3.12216e+190 b 4.826e+189` |

## As quatro perguntas do slide 11

**1. A perda está caindo a cada passo, ou oscilando?**

R: Com 0,001 e 0,1, a perda cai a cada passo. Com 1,5, ela aumenta já do passo 1 para o 2 (de 284802 para 2.14358e+07) e continua crescendo; não oscila em torno de um valor menor, diverge.

**2. Ela estabiliza, ou continua descendo até o fim?**

R: Com 0,1, estabiliza em cerca de 0.752176 por volta do passo 50. Com 0,001, ainda está descendo no passo 200. Com 1,5, não estabiliza: a perda cresce até chegar a `inf`.

**3. Os pesos encontrados batem com os que geraram os dados?**

R: Com 0,1, sim: w=300.008 e b=4.91185 ficam próximos dos valores verdadeiros (w=300 e b=5). Com 0,001, ainda não: w=215.016 e b=-17.7381 estão distantes após 200 passos. Com 1,5, não; os pesos divergem.

**4. Se algo divergiu, qual foi o primeiro passo estranho?**

R: Na taxa 1,5, o primeiro passo estranho é o passo 2, quando a perda salta de 284802 para 2.14358e+07. Ela continua crescendo e já é `inf` no passo 199.
