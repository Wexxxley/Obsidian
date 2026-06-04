
#Concluded 

---
### **Topologia em barramento**
- Todos os dispositivos são conectados a um **único cabo principal**. Em cada extremidade do cabo, há um "terminador" para impedir que o sinal reflita . Quando um computador envia dados, o sinal viaja por todo o cabo e todos os outros computadores o recebem (broadcast), mas apenas o destinatário com o endereço correto processa a informação.
- **Baixo Custo:** É a topologia mais barata e simples de instalar, pois utiliza uma quantidade mínima de cabo.
- **Fácil Instalação:** Basta estender o cabo principal e conectar os dispositivos a ele.

- **Falhas:** Se houver uma ruptura no cabo principal, **toda a rede para de funcionar**. 
- **Alto Tráfego e Colisões:** Como todos os dispositivos compartilham o mesmo meio de transmissão, o risco de colisões é alto.

![200](../../../../attachments/Pasted%20image%2020250701164558.png)

### **Topologia estrela**
- Possui um elemento central (hub ou switch) e todos os nós estão conectados a ele.  Toda a comunicação passa obrigatoriamente por este dispositivo central, que se encarrega de encaminhar os dados ao destino correto.
- **Fácil gerenciamento**: Como tudo está centralizado, é mais fácil adicionar ou remover dispositivos e identificar problemas.
- **Isolamento de Falhas:** Se um cabo ou um computador falhar, apenas aquele dispositivo fica fora da rede. O restante da rede continua funcionando normalmente.
- **Bom Desempenho:** Com o uso de um switch como nó central, as colisões são drasticamente reduzidas, pois ele cria canais de comunicação diretos entre a origem e o destino.

- **Ponto Único de Falha:** Esta é a principal desvantagem. Se o dispositivo central falhar, **toda a rede para de funcionar**.
- **Custo e Instalação:** Requer mais cabos do que a topologia em barramento, pois cada dispositivo precisa de um cabo exclusivo até o ponto central.
- 100 m é a distância máxima (cabos) entre os nós e o hub.

![200](../../../../attachments/Pasted%20image%2020250701164252.png)

### **Topologia em anel**
- Cada dispositivo é conectado diretamente a outros dois, formando um anel físico. Os dados viajam de nó em nó. Cada computador atua como um repetidor, recebendo o sinal, regenerando-o e passando-o para o próximo dispositivo até que ele chegue ao seu destino.
- Os dados passam pelos máquinas mesmo que elas estejam desligadas.
- Pode ter várias pontos de falho nos enlaces que ainda funciona de forma segmentada.

- **Dificuldade na Manutenção:** gerenciamento e manutenção mais complexos.
- **Custo alto** se comparado ao barramento

![200](../../../../attachments/Pasted%20image%2020250701164839.png)

