

---
, são a parte mais visível de uma rede estruturada.

### **1. As Tomadas de Rede**

As **Caixas conectoras/Tomadas de rede/Conectores fêmea RJ-45** são o ponto final da fiação de rede em um ambiente, como uma sala.
- A função é **fornecer um ponto de conexão fixo** e padronizado na parede para que um usuário possa conectar seu dispositivo à rede.
- Por trás dessa tomada, existe um cabo de rede chamado de cabo de instalação que passa por dentro de paredes. Esse cabo conecta a tomada de rede até uma sala central de equipamentos
![200](../../attachments/Pasted%20image%2020250703193850.png)
### **2. O Patch Panel**
- É um painel que fica em um rack de equipamentos. Cada porta no Patch Panel corresponde a uma tomada em algum lugar da edificação.
- A outra ponta daquele cabo de rede rígido que saiu da tomada da parede é conectada na parte de trás do Patch Panel.
- Em vez de ter dezenas de cabos longos e bagunçados chegando diretamente no switch, você tem um painel limpo e organizado. Todas as conexões da infraestrutura terminam ali.
  ![250](../../attachments/Pasted%20image%2020250703194115.png)
### **3. O Patch Cord**
- É o cabo de rede curto e flexível com conectores macho RJ-45 nas duas pontas.
- A função é fazer as conexões finais e "ativar".
    
- **Onde é usado (em dois lugares):**
    
    1. **Na Sala do Usuário:** Para conectar o computador do usuário à **tomada de rede** na parede.
        
    2. **No Rack de Equipamentos:** Para conectar a porta do **Patch Panel** (que representa a tomada da sala) à porta de um **Switch** (o equipamento que distribui a rede).
        

---

### A Relação: O Caminho Completo do Sinal

Agora, vamos juntar tudo e seguir o caminho que os dados percorrem:

1. O **Computador** do usuário é conectado com um **Patch Cord** (cabo flexível)...
    
2. ...na **Tomada de Rede** na parede da sala.
    
3. O sinal viaja pelo cabo de instalação permanente dentro da parede...
    
4. ...até a parte de trás do **Patch Panel** no rack central.
    
5. Da porta frontal do Patch Panel, outro **Patch Cord** (cabo flexível) é usado para conectar...
    
6. ...à porta do **Switch**, que finalmente conecta o computador à rede principal e à internet.
    

**Diagrama do Fluxo:**

`[Computador] <--> [Patch Cord] <--> [Tomada na Parede] ----(Cabo Permanente)----> [Patch Panel] <--> [Patch Cord] <--> [Switch]`

### Vantagens dessa Relação

- **Organização:** Mantém a sala de equipamentos limpa e fácil de gerenciar.
    
- **Flexibilidade:** Precisa mudar a qual porta do switch uma sala está conectada? Basta mover um pequeno Patch Cord no rack. Não precisa mexer na fiação dentro da parede.
    
- **Durabilidade:** O cabo caro e difícil de passar (o permanente, dentro da parede) fica protegido. O desgaste de conectar e desconectar acontece nos Patch Cords, que são baratos e fáceis de substituir.
    
- **Manutenção:** Facilita a identificação de problemas. É possível testar o link do Patch Panel até a tomada para ver se o cabo permanente está funcionando.

