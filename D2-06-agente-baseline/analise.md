### Saída do terminal ao rodar o arquivo "medir.py", utilizando o "casos-de-reserva.csv"
```bash
    
Métrica primária: acerto da decisão (casos com decisão igual à rotulada, sobre o total)
Valor: 25/30 = 0.8333
Conjunto: casos-de-reserva.csv — 30 casos rotulados {'seguir_operando': 16, 'parar_para_manutencao': 7, 'inspecionar_antes_de_operar': 7}
Onde erra (o rótulo que o agente não deu):
  caso C07: decidiu seguir_operando, correto era inspecionar_antes_de_operar
  caso C08: decidiu seguir_operando, correto era inspecionar_antes_de_operar
  caso C10: decidiu inspecionar_antes_de_operar, correto era seguir_operando
  caso C11: decidiu parar_para_manutencao, correto era inspecionar_antes_de_operar
  caso C22: decidiu parar_para_manutencao, correto era inspecionar_antes_de_operar

```

### Onde o agente erra e o por quê?
Nos casos C07, C08, C11 e C22, o agente não avalia bem o risco e acaba deixando de fazer inspeções necessárias. Já no C10, faz uma inspeção desnecessária por considerar falhas anteriores do TORNO, sem avaliar o menor risco da situação atual. Isso mostra que as regras fixas do arquivo medir.py são aplicadas de forma muito generalizada.