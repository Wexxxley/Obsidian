

---
Existe um "abismo" de velocidade entre os componentes. A CPU opera em nanossegundos, enquanto a RAM opera em dezenas ou centenas de nanossegundos. Para a CPU, esperar pela RAM é como se você tivesse que esperar 10 minutos por um papel que está na sua própria mesa.

### **1. Cache**

<mark style="background: #ADCCFFA6;">O Cache é uma quantidade muito pequena de memória extremamente rápida (e cara) que fica localizada _dentro_ do próprio chip da CPU ou muito, muito perto dela.</mark>

A função do cache é armazenar os dados e instruções que a CPU acabou de usar ou que ela _provavelmente_ usará no próximo instante.

**Níveis de Cache (L1, L2, L3)**

- **Cache L1:** É o menor e mais rápido. Fica _dentro_ de cada núcleo da CPU.
- **Cache L2:** Um pouco maior e um pouco mais lento. Fica logo ao lado do núcleo. 
- **Cache L3:** É o maior dos caches e é compartilhado por _todos_ os núcleos da CPU. 

---
### **Hierarquia Completa**

O fluxo de dados em um computador moderno segue esta ordem, do mais rápido para o mais lento:

1. **CPU (Registradores):** Onde o cálculo acontece _agora_.
    
2. **Cache L1** (Kilobytes)
    
3. **Cache L2** (Kilobytes/Megabytes)
    
4. **Cache L3** (Megabytes)
    
5. **RAM** (Gigabytes)
    
6. **Armazenamento (SSD/HDD)** (Gigabytes/Terabytes)
    

O objetivo de todo o sistema é manter esse funil sempre cheio, para que a CPU (no topo) nunca pare de trabalhar esperando por dados que estão lá embaixo.