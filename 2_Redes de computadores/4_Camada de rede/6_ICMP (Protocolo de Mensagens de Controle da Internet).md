

---

**O ICMP é usado por hosts e roteadores para troca de informação de controle da camada de rede.**

- **Usado por hosts e roteadores:** O ICMP é utilizado tanto por dispositivos finais quanto por roteadores.
- **Error reporting:** Quando algo dá errado com a entrega de um pacote IP o ICMP é usado para enviar uma mensagem de volta ao remetente.
- **Echo request/reply:** O comando `ping` envia uma mensagem ICMP **Echo Request** para um host de destino, se o host estiver acessível, ele responde com uma mensagem **ICMP Echo Reply.** Isso é comumente usado para testar a conectividade da rede e medir o tempo de ida e volta.
- **Transporte de mensagens:** As mensagens ICMP são encapsuladas dentro de datagramas IP. Isso significa que uma mensagem ICMP é a "carga útil" de um pacote IP.

---

### **Tabela de Mensagens ICMP**

| Tipo | Código | Descrição                | Observações                                             |
| :--- | :----- | :----------------------- | :------------------------------------------------------ |
| 0    | 0      | **Echo Reply**           | Resposta ao comando `ping`.                             |
| 3    | 0      | **Network Unreachable**  | A rede de destino não pode ser alcançada.               |
| 3    | 1      | **Host Unreachable**     | O host de destino não pode ser alcançado.               |
| 3    | 2      | **Protocol Unreachable** | Protocolo solicitado não disponível no host de destino. |
| 3    | 3      | **Port Unreachable**     | Porta solicitada não disponível no host de destino.     |
| 3    | 6      | **Dest Network Unknown** | A rede de destino é desconhecida.                       |
| 8    | 0      | **Echo Request**         | Usado pelo `ping` para testar a conectividade.          |
| 9    | 0      | **Router Advertisement** | Roteadores anunciam sua presença.                       |
| 10   | 0      | **Router Solicitation**  | Hosts solicitam anúncios de roteador.                   |
| 11   | 0      | **TTL Expired**          | O campo TTL do pacote atingiu zero.                     |
| 12   | 0      | **IP Header Bad**        | O cabeçalho IP contém um erro.                          |

---
### **Traceroute e ICMP**

O comando `traceroute` é uma ferramenta de diagnóstico de rede usada para **rastrear a rota que os pacotes percorrem de um computador de origem até um destino específico**

1. O transmissor **envia uma série de segmentos UDP** com TTL 1, 2, 3 e assim sucessivamente. Os pacotes são enviados para um número de **porta de destino que é improvável de estar em uso.** Isso é crucial para a interrupção.
2. Cada pacote com TTL baixo "morre" em um roteador, fazendo com que esse roteador envie uma mensagem ICMP "**TTL Expirado**" de volta à origem. A mensagem ICMP contém informações sobre o roteador que a enviou, o que permite ao `traceroute` identificar cada "salto" no caminho.
3. A origem usa essas mensagens ICMP para identificar cada roteador no caminho e calcular o **RTT (Round Trip Time)**, ou seja, o tempo de ida e volta para cada um.
4. Quando o pacote finalmente chega ao destino final. o destino responde com uma mensagem ICMP "**Porta Inalcançável**" (já que nenhuma aplicação está ouvindo na porta improvável).
5. Essa mensagem "Porta Inalcançável" sinaliza ao `traceroute` que ele chegou ao destino, e o processo termina.