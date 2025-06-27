
---

---

### **1. Função da placa de rede** 
O coração da comunicação é o **adaptador**, também conhecido como Placa de Interface de Rede (NIC). A Camada de Enlace de Dados é **implementada diretamente nesse adaptador**.
- **Cartão Ethernet**: Tipo de NIC para redes cabeadas.
- **Cartão PCMCIA**: Um tipo mais antigo de adaptador, usado principalmente em laptops para diversas funções, incluindo rede.
- **Cartão 802.11**: Refere-se a um adaptador Wi-Fi.

Esses adaptadores são a ponte entre o seu computador e o meio físico da rede (cabo ou ar).

![[Pasted image 20250627100949.png]]

**Lado Transmissor:**
1. **Encapsula o datagrama em um quadro:**
    - Quando seu computador quer enviar dados, a **Camada de Rede** entrega um **datagrama** para a **Camada de Enlace**.
    - O adaptador (NIC) então pega esse datagrama e o **encapsula** dentro de um **quadro (frame)**. 
**Lado Receptor:**
2. **Procura erros, controle de fluxo etc...:**
    - O adaptador do lado receptor recebe o quadro do enlace físico.
    - Ele primeiro verifica os bits de verificação de erro para ver se o quadro chegou intacto. Se houver erros não corrigíveis, o quadro pode ser descartado ou uma retransmissão pode ser solicitada.
    - Informa ao transmissor se está pronto para receber mais dados.
3. **Extrai o datagrama, passa para o lado receptor:**
    - Se o quadro estiver OK e for destinado a ele, o adaptador receptor **desencapsula** o quadro, removendo o cabeçalho e o rodapé da camada de enlace.
    - Esse datagrama é então entregue à **Camada de Rede** do dispositivo receptor.

---
### **2. O Papel dos Drivers**

- Um **driver** é um software que atua como uma interface entre o sistema operacional do seu computador e o hardware do adaptador (NIC).
- Quando o sistema operacional precisa enviar um datagrama, ele passa essa informação ao driver da placa de rede. O driver instrui o hardware da placa a realizar todas as operações.
- Da mesma forma, quando a placa de rede recebe bits do meio físico, o driver os interpreta, lida com a detecção de erros, desencapsula o datagrama e o passa para o sistema operacional, que o encaminha para as camadas de rede e transporte.

Sem o driver correto, o sistema operacional não consegue "conversar" com a placa de rede, e a comunicação não seria possível. 