# O meu dado, com rigor — relatório do Laboratório 03

Conjunto: `meus_casos.csv` · 60 linhas · 11 variáveis

Medidas geradas pelo `medidas.py`: desvio padrão amostral (ddof=1),
quartis por interpolação linear, extremos pela regra da amplitude
interquartil — fora de 1,5 × a caixa (slide 24). As medidas são do
programa; as decisões são SUAS. Preencha todos os blocos `R:` e
confira com `python teste.py`.

## Medidas por variável

| variável | tipo | n | faltantes | média | mediana | desvio | Q1 | Q3 | AIQ | mín | máx |
|---|---|---:|---:|---:|---:|---:|---:|---:|---:|---:|---:|
| id_caso | categórica (60 valores; moda: C11) | 60 | 0 | — | — | — | — | — | — | — | — |
| data | categórica (30 valores; moda: 2026-03-06) | 60 | 0 | — | — | — | — | — | — | — | — |
| variante_produto | categórica (3 valores; moda: L) | 60 | 0 | — | — | — | — | — | — | — | — |
| temperatura_c | numérica | 60 | 0 | 37.1417 | 37.0000 | 1.5239 | 36.0250 | 38.2750 | 2.2500 | 34.3500 | 40.2500 |
| rpm | numérica | 60 | 0 | 1634.0167 | 1506.0000 | 379.6243 | 1375.2500 | 1674.5000 | 299.2500 | 1289.0000 | 2678.0000 |
| torque_nm | numérica | 60 | 0 | 41.5817 | 43.3000 | 16.2623 | 30.1500 | 53.2750 | 23.1250 | 10.7000 | 67.1000 |
| potencia_w | numérica | 60 | 0 | 6533.3833 | 6733.5000 | 1729.0701 | 5386.5000 | 7778.2500 | 2391.7500 | 3000.0000 | 9311.0000 |
| desgaste_ferramenta_min | numérica | 60 | 0 | 128.9833 | 149.0000 | 83.3277 | 40.2500 | 206.0000 | 165.7500 | 0.0000 | 240.0000 |
| acao_correta | categórica (3 valores; moda: seguir_operando) | 60 | 0 | — | — | — | — | — | — | — | — |
| falhou_depois | numérica | 60 | 0 | 0.2667 | 0.0000 | 0.4459 | 0.0000 | 1.0000 | 1.0000 | 0.0000 | 1.0000 |
| dificuldade | categórica (5 valores; moda: dificil) | 60 | 0 | — | — | — | — | — | — | — | — |

## Extremos marcados (fora de 1,5 × a caixa — slide 24)

### Extremos de `rpm` — 9 valor(es), limites [926.3750; 2123.3750]

| linha | valor |
|---:|---:|
| 2 | 2678.0000 |
| 10 | 2355.0000 |
| 22 | 2370.0000 |
| 24 | 2595.0000 |
| 36 | 2482.0000 |
| 41 | 2398.0000 |
| 46 | 2610.0000 |
| 52 | 2427.0000 |
| 57 | 2346.0000 |

Decisão sobre ESTES extremos — manter ou remover, caso a caso,
com o motivo (slide 25: quem remove sem dizer, mente por omissão):

R: Manter os 9 casos. Todos têm RPM alto, torque e potência baixos e estão
marcados como atípicos; não há evidência de erro de medição.


## Faltantes (os três mecanismos do slide 26)

Nenhuma variável tem valores faltantes.

## As quatro perguntas do slide 29

**1. Média e mediana se separam em alguma variável? Em qual?**

R: Sim. Em RPM, a média (1634) supera a mediana (1506). Em potência (6533
contra 6734) e desgaste (129 contra 149), a média fica abaixo da mediana.

**2. Quantos extremos foram marcados, e quantos você decidiu manter?**

R: Foram marcados 9 extremos de RPM; decidi manter os 9 por representarem
casos atípicos relevantes, não erros comprovados.

**3. Algum faltante parece do terceiro mecanismo?**

R: Não. O conjunto não tem valores faltantes.

**4. O que a análise da D1 não tinha visto?**

R: A amostra ampliada evidencia 9 casos de RPM elevado acompanhados por
torque e potência baixos, um padrão de operação atípico.

## Comparação com a análise exploratória da D1

O que mudou de lá para cá — o que a análise de lá não tinha visto,
e o que estas decisões escritas mudam no conjunto que a D5 vai usar:

R: Com a inclusão dos 30 novos casos, a base passou a ter 60 registros e foram identificados 9 valores extremos de RPM. Esses valores serão mantidos para que também sejam considerados na análise, já que representam situações fora do padrão. Além disso, não há dados faltantes na base.
