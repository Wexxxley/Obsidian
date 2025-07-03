

---
O problema da sincronização global do TCP ocorre quando múltiplas sessões TCP, que atravessam um mesmo roteador congestionado, perdem pacotes **ao mesmo tempo** e, consequentemente, **reduzem suas taxas de envio simultaneamente**. Quando voltam a normalizar aumetam ao a taxa de tranferencia ao mesmo tempo causando um ciclo de subir a taxa de tranferencia e descer a taxa de tranferencia

![Pasted image 20250606105830](../../attachments/Pasted%20image%2020250606105830.png)

1. **Fila cheia:** Várias sessões TCP estão enviando dados através de um roteador. A taxa de chegada de pacotes ao buffer de saída do roteador excede a capacidade de saída do link.
2. **Descarte em Massa:** A fila atinge sua capacidade máxima. O roteador começa a descartar todos os pacotes que chegam subsequentes. Crucialmente, como o descarte ocorre no final da fila.
3. **Detecção de Perda e Reação Sincronizada:** Cada uma das sessões TCP que perdeu pacotes detecta essa perda via ACKs duplicados. Como reação, todas essas sessões TCP simultaneamente entram em suas fases de controle de congestionamento, reduzindo suas janelas de congestionamento e, portanto, suas taxas de envio.
4. **Baixa sincronizada:** Com muitas sessasões desacelerando ao mesmo tempo, o link que estava congestionado de repente fica **subutilizado**. 
5. **Aumento Sincronizado:** Como todas as sessões estão aumentando suas taxas de envio ao mesmo tempo, elas rapidamente voltam a congestionar o mesmo roteador.
