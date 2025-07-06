#Concluded 

---
### **1. Função da placa de rede** 

O coração da comunicação é o **adaptador**, também conhecido como Placa de Interface de Rede (NIC). A camada de enlace é "implementada" no adaptador.

Esses adaptadores são a ponte entre o seu computador e o meio físico da rede.

![Pasted image 20250627100949](../../attachments/Pasted%20image%2020250627100949.png)

**Lado Transmissor:**

1. **Encapsula o datagrama em um quadro:**
    - Quando seu computador quer enviar dados, a **Camada de Rede** entrega um **datagrama** para a **Camada de Enlace**. O adaptador então pega esse datagrama e o **encapsula** dentro de um **quadro (frame)**. 
**Lado Receptor:**
2. **Procura erros e controle de fluxo:**
    - A adaptador receptor primeiro verifica os bits de verificação de erro. Se houver erros não corrigíveis, o quadro pode ser descartado ou uma retransmissão pode ser solicitada.
    - Informa ao transmissor se está pronto para receber mais dados.
3. **Extrai o datagrama, passa para o lado receptor:**
    - Se o quadro estiver OK e for destinado a ele, o adaptador receptor **desencapsula** o quadro, removendo o cabeçalho e o rodapé da camada de enlace.
    - Esse datagrama é então entregue à **Camada de Rede** do dispositivo receptor.

---
### **2. O Papel dos Drivers**

- Um **driver** é um software que atua como uma interface entre o sistema operacional e o hardware do adaptador (NIC).
- Quando o sistema operacional precisa enviar um datagrama, ele passa essa informação ao driver da placa de rede. O driver instrui o hardware da placa a realizar todas as operações.
- Quando a placa de rede recebe bits do meio físico, o driver os interpreta, lida com a detecção de erros, desencapsula o datagrama e o passa para o sistema operacional, que o encaminha para as camadas de rede e transporte.
- A vantagem dos drivers é felixibilidade visto que eles podem receber atualizações. E a tendência é que os adaptadores sejam mais genéricos.
