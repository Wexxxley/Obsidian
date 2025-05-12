

---
# Segmento tcp
![[Pasted image 20250509134237.png]]

- O campo de opções, opcional e de comprimento variável, é usado quando um remetente e um destinatário negociam o MSS, ou como um fator de aumento de escala da janela para utilização em redes de alta velocidade. 
- O campo de **flag** contém 6 bits. O bit **ACK** é usado para indicar se o valor carregado no campo de reconhecimento é válido, isto é, se o segmento contém um reconhecimento para um segmento que foi recebido com sucesso. 

**Buffers de envio de recepção**
![[Pasted image 20250509133804.png]]

---
# Apresentação TCP

**Número de sequência e de reconhecimento**
O **número de sequência** para um segmento é o número do primeiro byte do segmento. Suponha que um processo no hospedeiro A queira enviar uma cadeia de dados para um processo no hospedeiro B. O TCP do hospedeiro A vai implicitamente numerar cada byte da cadeia de dados. Suponha que a cadeia de dados consista em um arquivo composto de 500 mil bytes, que o MSS(maximun segment size) seja de 1.000 bytes e que seja atribuído o número 0 ao primeiro byte.

O TCP constrói 500 segmentos a partir da cadeia de dados. O primeiro recebe o número de sequência 0; o segundo, o número de sequência 1.000; e assim por diante. Cada número de sequência é inserido no campo de sequência no cabeçalho do segmento. 

Vamos agora considerar os **números de reconhecimento**. O número de reconhecimento que o hospedeiro A atribui a seu segmento é o número de sequência do próximo byte que ele estiver aguardando do hospedeiro B.
![[Pasted image 20250509135245.png]]

**Conexão**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcgpiDavS7LfwXV22ihWijvZYhrty_8AA8D21QLJ2QHzwtTIgY-Lq6BNCHsH5j2elmZWCQxrWjsIALs5-z2Yg_ZKl7XZHVCvteH6WMcqGSiXIyKpPx9lZlmNENNBp-jnqqSI5nN?key=HrOhHC0_-ked6RNCpQ0o3PZn)
- **SYN**: Synchronize: basicamente um pedido para conexão
- **ACK**: Acknowledge: utilizado para confirmar que a mensagem foi recebida

**Finalização de conexão**
![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXfwbd7HwmpbmP9PEwLkcUElrWyP_aTmex_rQ7sATRmDbv98rJbmcw9fBbwYqCTnyOv55iUgdcs9rX6dUkpnPBv7055BKlupdyiF3yOg71HMI9LISZWXl9XzTMf2vLgBeAhqROittA?key=HrOhHC0_-ked6RNCpQ0o3PZn)
O cliente avisa que não vai mais enviar nada. E o server confirma que recebeu, mas o server ainda pode ficar enviando pacotes até que ele decida não querer mais conexão.

---

# Cenários de retransmissão

**Cenário de esgotamento de temporização**
![[Pasted image 20250509140214.png]]

**Reconhecimento acumulativo**
![[Pasted image 20250509140546.png]]

**Retransmissão de dados**
![[Pasted image 20250509140658.png]]
