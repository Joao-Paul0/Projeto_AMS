# O mapa do meu domínio — conferência (Laboratório 04)

Conjunto: manutencao · 384 dimensões antes da redução
Escolha registrada (slide 55): normalizado · semente da vizinhança: 20260901
Mapas: mapa-do-espaco.png (componentes principais à esquerda, vizinhança à direita) · pontos: mapa-pontos.csv

## Passo 4 — os três pares que você escolheu no mapa (slide 52)

| par | cosseno original | a vizinhança visual |
|---|---|---|
| (35, 36) | +0.9780 | confirma |
| (60, 77) | +0.1228 | NÃO confirma |
| (20, 21) | +0.5950 | confirma |

## As quatro perguntas do slide 53

1. Os dois métodos produzem os mesmos agrupamentos?
R: Sim, em linhas gerais eles apontam para os mesmos agrupamentos, mas o PCA preserva melhor a estrutura global enquanto o t-SNE enfatiza grupos locais e distorce as distâncias entre grupos.

2. Há grupo que só aparece em um deles?
R: Sim. O t-SNE cria grupos bem mais nítidos e separa regiões locais que no PCA aparecem mais misturadas; isso é o efeito do foco em vizinhos próximos, não em distâncias globais.

3. Os vizinhos visuais confirmam no cosseno original?
R: Parcialmente. Os pares (35, 36) e (20, 21) confirmaram com cossenos +0.9780 e +0.5950, mas (60, 77) parecia vizinho no mapa e, no espaço original, deu apenas +0.1228, então a vizinhança visual pode enganar.

4. O que aconteceria com um vetor novo, fora do conjunto?
R: No mapa de componentes principais, ele seria posicionado por uma projeção fixa: (v − centro) @ componentes. No t-SNE não há posição pronta para um novo vetor, porque o mapa inteiro depende do conjunto original e precisaria ser refeito.

## O caso em que o mapa enganou (critério do slide 52)

Par e o que a figura sugeria, e o que o cosseno original disse:

R: O par (60, 77) parecia próximo na vizinhança, mas o cosseno original foi +0.1228, bem abaixo de 0.5; a figura sugeriu vizinhança, porém o espaço original mostrou que eles eram bem diferentes.
