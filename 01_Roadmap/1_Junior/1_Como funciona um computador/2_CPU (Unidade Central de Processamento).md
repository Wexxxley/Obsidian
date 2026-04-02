
#Concluded 

---

A CPU (_Central Processing Unit_) é, sem dúvida, o componente mais importante. 

### **1. O que a CPU faz?**

- A CPU é o componente que **executa instruções**. Ela que<mark style="background: #ADCCFFA6;"> realiza calculos lógicos e matemáticos</mark>
- Quando você pede para somar 2 + 2, é a CPU quem faz o cálculo. Quando você move o mouse, é a CPU que calcula a nova posição do cursor.
- Ela busca dados da memória, processa esses dados e, em seguida, envia o resultado de volta para a memória ou para um dispositivo.
- A velocidade da CPU é medida em **Gigahertz (GHz)**. Um processador de 3.1 GHz pode, teoricamente, realizar 3.1 bilhões de operações básicas por segundo.

![](../../../attachments/Pasted%20image%2020251027111531.png)

---
### **2.  Núcleos/Cores**

- Antigamente, uma CPU tinha apenas um "cérebro" e só podia fazer uma única coisa de cada vez. Os engenheiros descobriram como colocar _várias CPUs_ dentro de um único chip. Cada uma dessas CPUs internas é chamada de **Núcleo (Core)**.
- Um computador "dual-core" pode, literalmente, fazer duas coisas ao mesmo tempo. Um "quad-core" pode fazer quatro.
- É por isso que hoje você pode ouvir música, navegar na internet e ter um antivírus rodando ao fundo, tudo ao mesmo tempo e sem que o computador trave. Cada núcleo pode estar cuidando de uma tarefa diferente.

---
### **3. O que é "Hyper-Threading"?**

- O _Hyper-Threading_ (tecnologia da Intel) é um truque inteligente para fazer um único núcleo físico se parecer com _dois_ núcleos para o sistema operacional.    
- O núcleo é tão rápido que consegue fazer duas tarefas ao mesmo tempo alternando muito rapidamente. 
- Um processador com 2 núcleos físicos e Hyper-Threading aparecerá para o Windows como tendo 4 processadores. Isso otimiza o uso do núcleo, garantindo que ele esteja sempre ocupado e não fique ocioso esperando por dados.

---
### **4. Meu processador**

Meu processado atual é um **AMD Ryzen 7 5700U**:

- **Cores:** Ele possui **8 núcleos** físicos. Esse processador pode, literalmente, trabalhar em 8 tarefas físicas diferentes ao mesmo tempo.

- **Threads da CPU:** Ele possui **16 threads**. Isso acontece graças à tecnologia da AMD chamada **SMT (Simultaneous Multithreading)**. Ela permite que cada um desses 8 núcleos físicos se comporte como _dois_ núcleos lógicos para o sistema operacional. Isso permite que o processador gerencie 16 "filas de tarefas" (threads) de uma vez.

