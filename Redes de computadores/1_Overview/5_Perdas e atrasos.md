
Status: #Concluded 

___

1. **Processamento de chegada:** O pacote chega pela interface de entrada do roteador. Aqui começa o atraso de recepção, que é mínimo.
2. **Enfileiramento de Chegada:** Se muitos pacotes estão chegando ao mesmo tempo, o roteador precisa colocar os pacotes em uma fila de espera até poder processá-los. Isso gera um atraso e ,caso a fila esteja cheia, o pacote é descartado.
3. **Processamento de Roteamento:** O roteador lê o cabeçalho do pacote e decide para onde encaminhar, o que leva um tempo mínimo.  
4. **Fila de Saída:** Depois de processado, o pacote vai para a fila de saída, aguardando sua vez de ser enviado para o próximo roteador. É aqui onde ocorrem os atrasos e variações mais significativas.  
5. **Serialização:** Agora é hora de enviar o pacote bit a bit pelo meio.  
6. **Atraso de Propagação:** Depois de sair do roteador, o pacote viaja fisicamente pelo meio até o próximo roteador.

[[1_Por dentro do roteador]]