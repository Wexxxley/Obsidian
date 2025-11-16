#Concluded 

---
### **1. Protocolo IP vs. Endereço IP**

- **IP - Internet Protocol:** É o conjunto de padrões que define como os dados devem ser formatados e enviados pela internet. Ele é a parte da arquitetura TCP/IP e atual na camada de rede.
    
- **Endereço IP:** É o identificador numérico que o protocolo usa para saber para onde enviar os dados.

---
### **2. O Endereço IP é Globalmente Exclusivo?**

- **SIM (Endereço IP Público):** O endereço IP que o seu provedor de internet (ISP) dá ao seu roteador é globalmente único. Nenhum outro dispositivo no mundo pode ter esse mesmo IP público naquele momento.
    
- **NÃO (Endereço IP Privado):** O endereço IP que o seu roteador dá aos seus dispositivos dentro da sua casa não é globalmente único. Milhões de laptops em milhões de casas diferentes têm exatamente o mesmo IP privado.
    
Isso funciona graças ao NAT (Network Address Translation): [8_NAT](8_NAT.md)

---
### **3. O que o Protocolo IP faz, de Fato?**

A função real do Protocolo IP é <mark style="background: #BBFABBA6;">endereçar e rotear pacotes.</mark>

1. Um protocolo da camada de cima (como o TCP) entrega ao IP um bloco de dados.
    
2. O Protocolo IP pega esse bloco e o "encapsula" em um Pacote IP. A parte mais importante que ele adiciona é o **IP Header**.
    
3. Esse cabeçalho contém, entre outras coisas:
    - **Endereço IP de Origem**
    - **Endereço IP de Destino**
        
4. O IP envia o pacote para o primeiro roteador. Esse roteador lê o IP de Destino, consulta sua tabela de roteamento e envia o pacote para o próximo roteador. Isso se repete várias vezes até chegar ao destino.
    

---
### **4. IP não é Confiável**

O Protocolo IP por si só não garante _nada_.
- Ele não garante que o pacote vai chegar.
- Ele não garante que os pacotes chegarão na ordem correta.
- Ele não pede reenvio se um pacote se perder.

É o trabalho do protocolo da camada de t (o protocolo da camada de cima) receber os pacotes do IP, organizá-los, verificar se falta algum, pedir o reenvio (ex: "Ei, Google, o pacote 1 de 4 não chegou!") e garantir que a foto do gato seja montada corretamente.
### **1. Campos**

 Um pacote de camada de rede é denominado um **datagrama**. Os principais campos do datagrama ipv4 são os seguintes: 

 - **Número da versão** 
 - **Comprimento cabeçalho:** Um datagrama IPv4 pode conter um número variável de opções, esses bits são necessários para determinar onde, no datagrama, os dados começam de fato. Normalmente datagramas não usam opções; o datagrama típico tem um cabeçalho de **2 bytes.**
 - **Tipo de serviço:** Usados para poder diferenciar os diferentes tipos serviço (que requerem baixo atraso, alta vazão ou confiabilidade) 
 - **Comprimento do datagrama.** É o comprimento total do datagrama (cabeçalho mais dados).
 - **Identificador, flags, deslocamento de fragmentação:** Campos usados na fragmentação.
 - **Tempo de vida:** Na prática, esse campo é decrementado em uma unidade cada vez que o datagrama é processado por um roteador, ou seja, virou um ==número máximo de saltos.==

![Pasted image 20250523103049](../../attachments/Pasted%20image%2020250523103049.png)

- **Protocolo:** O campo indica o protocolo de camada de transporte.
- **Soma de verificação:** A soma de verificação auxilia um roteador na detecção de errs de bits. 
- **Endereços IP de origem e de destino.**
- **Opções**: A intenção é que as opções de cabeçalho sejam usadas raramente.
- **Dados:** Contém o segmento da camada de transporte (TCP ou UDP) a ser entregue ao destino. Contudo, o campo de dados pode carregar outros tipos de dados, como mensagens ICMP.

---
### **2. Classes do IPv4**

| Classes | Intervalo do Primeiro Octeto | Padrão dos Primeiros Bits | Uso Principal        |
| :------ | :--------------------------- | :------------------------ | :------------------- |
| **A**   | 0 - 127                      | `0`xxxxxxx                | Grandes redes        |
| **B**   | 128 - 191                    | `10`xxxxxx                | Médias/Grandes redes |
| **C**   | 192 - 223                    | `110`xxxxx                | Pequenas redes       |
| **D**   | 224 - 239                    | `1110`xxxx                | Multicast            |
| **E**   | 240 - 255                    | `1111`xxxx                | Experimental/Testes  |

As classes são calculadas com base no primeiro octeto de bits.