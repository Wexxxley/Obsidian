
#Concluded 

---
### **1. Campos**
 Um pacote de camada de rede é denominado um **datagrama**. Os principais campos do datagrama ipv4 são os seguintes: 
 - **Número da versão** 
 - **Comprimento cabeçalho:** Um datagrama IPv4 pode conter um número variável de opções, esses bits são necessários para determinar onde, no datagrama, os dados começam de fato. Normalmente datagramas não usam opções; o datagrama típico tem um cabeçalho de **2 bytes.**
 - **Tipo de serviço:** Usados para poder diferenciar os diferentes tipos serviço (que requerem baixo atraso, alta vazão ou confiabilidade) 
 - **Comprimento do datagrama.** É o comprimento total do datagrama (cabeçalho mais dados).
 - **Identificador, flags, deslocamento de fragmentação:** Campos usados na fragmentação.
 - **Tempo de vida:** Na prática, esse campo é decrementado em uma unidade cada vez que o datagrama é processado por um roteador, ou seja, virou um ==número máximo de saltos.==
![[Pasted image 20250523103049.png]]
- **Protocolo:** O campo indica o protocolo de camada de transporte.
- **Soma de verificação:** A soma de verificação auxilia um roteador na detecção de erros de bits. 
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