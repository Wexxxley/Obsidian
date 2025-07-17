
#Concluded 

---
**A camada de enlace tem a responsabilidade de transferir um quadro de um dispositivo para outro dispositivo vizinho sobre um enlace**. Enlace é um canal de comunicação que conecta nós (hospedeirso e roteadores) vizinhos.

- **Enlaces com fio:** Utilizam um **meio físico**, como cabos, para transmitir dados entre dispositivos. A transmissão ocorre por meio de sinais elétricos ou luz.
- **Enlaces sem fio (wireless):** Não utilizam cabos físicos, usam ondas eletromagnéticas para transmitir dados pelo ar. Sempre possui interferências.
---
## **Serviços da camada de enlace**

#### **1. Enquadramento**: 
- Encapsula **datagramas** em quadros acrescentando cabeçalhos.
- Implementa acesso ao canal se o meio é compartilhado. Isso significa que, se vários dispositivos estão usando o mesmo meio de comunicação o enquadramento garante que apenas um dispositivo transmita por vez para evitar colisões.
#### **2. Entrega confiável**
- Entrega confiável é muito associado ao TCP.
- Raramente usado em enlaces com baixa taxa de erro (como fibra óptica).
- Enlaces sem fio: altas taxas de erro.
#### **3. Controle de Fluxo** 
- O **controle de fluxo** serve para **limitar a taxa de transmissão** entre o transmissor e o receptor, garantindo que o receptor não seja sobrecarregado.
#### **4. Detecção de Erros** 

Erros são comuns e podem ser causados por diversos fatores, como:

- **Atenuação do sinal**: O sinal enfraquece ao longo do meio de transmissão.
- **Ruídos**: Interferências eletromagnéticas que alteram o sinal.
- Quando um receptor detecta a presença de um erro em um quadro ele **avisa o transmissor para reenviar o quadro perdido ou corrompido**. 
#### **5. Correção de Erros**  
- Permite que o receptor **identifique e corrija os bits sem precisar pedir a retransmissão**. Isso é feito com o uso de **algoritmos de correção.** A correção de erros é mais complexa e adiciona mais sobrecarga aos dados. Os algoritmos adicionam **bits de redundância** (informação extra) aos dados originais. 
####  **6. Simplex, Half-duplex e Full-duplex**: 
[7_Modos de transmissão de dados](2_Redes%20de%20computadores/1_Overview/7_Modos%20de%20transmissão%20de%20dados.md)




