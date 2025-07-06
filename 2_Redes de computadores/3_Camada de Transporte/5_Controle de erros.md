

___
# **1. Protocolos de controle de erro**

## **1.1 Go-Back-N**

 Protocolo onde o transmissor pode enviar até N pacotes consecutivos sem esperar ACKs para cada um. No entanto, se um pacote for perdido, todos os pacotes após ele serão reenviados.

Janela de envio: A janela representa a quantidade máxima de pacotes que o transmissor pode enviar sem esperar confirmação (ACK). A janela se desloca conforme os ACKs vão sendo recebidos.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcN9DluFiKNgS3khjwO7T6GZRzdeyQlMX6tpEtG2_OGTvgkLyWAjgQ3LJqZ49JjjlPoUwGCot-yEm1DIoWf6EizXBOIrjWN9FYKG0oHGP5aX5giU4oqLxRPpnUzmsKx1amwLUDVGA?key=HrOhHC0_-ked6RNCpQ0o3PZn)

Cada pacote enviado tem seu próprio temporizador. Se o temporizador de um pacote expira sem receber ACK, o transmissor reenvia o pacote e todos os subsequentes (por isso "Go-Back-N").

O receptor envia o ACK para o último pacote recebido em ordem.

- Exemplo: se recebe os pacotes 1, 2, 3, 4 corretamente, envia ACK 5
- Se o pacote 3 for perdido, mesmo que 4 e 5 cheguem, o receptor os ignora e continua manda ACK 3. isso força o transmissor a reenviar do 3 em diante.

---
## **1.2 Retransmissão seletiva**

 Mais eficiente que o Go-Back-N em redes com alta latência ou perda, porque evita o reenvio desnecessário de pacotes já entregues corretamente.

- O transmissor pode enviar vários pacotes antes de receber confirmações (ACKs).
- O receptor confirma cada pacote individualmente. Se um pacote é perdido, somente ele é reenviado, e não todos os seguintes.
- O receptor armazena os pacotes fora de ordem até que o pacote perdido chegue, e então os entrega na ordem correta à camada superior.  

O TCP é híbrido

- Possui ACKS cumulativos; Segmentos corretamente recebidos em ordem não são reconhecidos individualmente.
- Armazena segmentos recebidos corretamente e fora de ordem e retransmite somente segmentos não recebidos.

________________________________________________________________________
# **2. Controle de fluxo e congestionamento**

## **2.1 Controle de fluxo**

 O receptor tem um buffer de recepção. Nem sempre o receptor consegue processar os dados na mesma velocidade que os recebe. Para evitar que o buffer fique cheio e ocorra perda de dados, o TCP usa o controle de fluxo.  

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXcGlhawycTb2W5CmIn4M7VUlCDm6fB7Ja3CkhGD67TbPDcTAlBGqo7XdkG38CfmGWu4nTJ4WVuD5kwX9canZeZB6P52cGCpSw8C7UGs1da4djM1RdgXFIqUldRaFNmtAB2tSuySSg?key=HrOhHC0_-ked6RNCpQ0o3PZn)

Componentes da imagem:

- RcvBuffer: tamanho total do buffer de recepção.
- RcvWindow: indica quanto espaço ainda está disponível .
- Processo de aplicação: parte do sistema receptor que consome os dados do buffer.

 O receptor informa ao emissor, em cada ACK, o valor de RcvWindow. O transmissor só pode enviar dados que caibam Isso previne sobrecarga.

---
## **2.2 Controle de congestionamento**

### **2.2.1 Fim-a-Fim (End-to-End)**
- Não depende da rede (roteadores) para detectar congestionamento.
- O emissor TCP infere que há congestionamento observando:
	- Perda de pacotes (ex: ACKs não chegam ou chegam duplicados).
	- Atrasos crescentes no tempo de resposta.
- Quando detecta perda ou atraso ele reduz o tamanho da janela de envio.
- Mais reativo do que preventivo (espera o problema aparecer para agir) e pode demorar mais para estabilizar a rede.
- Abordagem usada pelo TCP.  
### **2.2.1 Controle de Congestionamento Assistido pela Rede**
- A própria rede (roteadores) participa do controle. Os roteadores informam aos emissores se estão sobrecarregados.
- Roteadores usam um bit para indicar consgestionamento.
- O host, ao receber essas informações, ajusta sua taxa de envio.
- Pode responder mais rapidamente ao congestionamento.
- Requer alterações na infraestrutura da rede (roteadores precisam colaborar).Mais complexo de implementar do que o modelo fim-a-fim.

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXeg0hmcsIDIz64WXMWhuYXSh3aGjYyh_nksQzuuJIYS_rGxW2U6cbzfheZ3TT2EBQKwgDmmocnh5djZPGI8DMF4ct6ekyMOPEjOQWT6MJWXKoC0sfKJ_pkL8hdfTv9RJjeugqG1WQ?key=HrOhHC0_-ked6RNCpQ0o3PZn)

**Modos de operação**
1. **Início Lento:** A janela começa com o tamanho de 1 MSS (máximo de bytes de dados que cabem em 1 pacote naquela conexão) e dobra de tamanho cada ACK recebido.
2. **Evitar Congestionamento:** aumenta o tamanho da janela em 1 MSS a cada ACK recebido.

![Pasted image 20250512193101](../../attachments/Pasted%20image%2020250512193101.png)  
**Critérios de mudança** 

- Tamanho da janela **passou do limite de início lento**: mudar para evitar congestionamento.
- **1 ACK duplicado:** indicativo de perda pequena, retransmitir pacote e diminuir o tamanho da janela pela metade e passar ao modo de evitar colisão.
- **3 ACKs duplicados ou estouro do temporizador:** indicativo de grave congestionamento, retransmitir pacote e passar ao modo de início lento.