# Pares que surpreenderam — Laboratório 01

> O slide 19 do D3-E1 pede DOIS casos anotados: um par PRÓXIMO sem razão
> aparente e um par DISTANTE que deveria estar junto. Eles voltam na D7,
> quando a turma montar o próprio índice de recuperação — escreva aqui e
> guarde este arquivo no seu repositório.

## Um par PRÓXIMO sem razão aparente

- Índices do par: (35, 36)
- As duas frases:
  - primeira: Afrouxe os parafusos do mancal em ordem cru…
  - segunda: "Aperte os parafusos do mancal em ordem cruz…
- Cosseno medido: 0.9780
- Por que essa proximidade surpreendeu:

R: O modelo identificou as frases como muito semelhantes porque considerou principalmente o contexto e a estrutura, dando pouco peso à troca do verbo. Porém, as ações são opostas: afrouxar e apertar.Isso pode gerar erros perigosos em buscas e deduplicações na manutenção industrial.
## Um par DISTANTE que deveria estar junto

- Índices do par: (26, 143)
- As duas frases:
  - primeira: Registre as horas-homem da intervenção no s…
  - segunda: O líquido penetrante nas soldas do tanque n…
- Cosseno medido:
- Por que essa distância surpreendeu:

R: O resultado surpreendeu porque a similaridade foi negativa, indicando que as frases estão em regiões diferentes do espaço vetorial

## O que a comparação com NORMALIZAR = True mudou

- Alguma ordem mudou? De qual par:

R: O que a comparação com NORMALIZAR = True mudou

- Alguma ordem mudou? De qual par:

R: A normalização manteve a ordem do cosseno e fez a distância euclidiana apresentar exatamente a mesma classificação dos pares, eliminando as diferenças que existiam antes.