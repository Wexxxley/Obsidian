

---
 O ICMP é usado pelos roteadores para troca de informação de controle da camada de rede. Indicando, por exemplo, que um serviço solicitado não está disponível ou que um host ou roteador não pôde ser alcançado.

**Usado por hosts e roteadores para troca de informação de controle da camada de rede.**

- **Usado por hosts e roteadores:** O ICMP é utilizado tanto por dispositivos finais (como seu computador) quanto por dispositivos intermediários (roteadores) para trocar informações de controle na camada de rede 
- **Error reporting:** Uma das funções primárias do ICMP é relatar erros. Quando algo dá errado com a entrega de um pacote IP o ICMP é usado para enviar uma mensagem de volta ao remetente informando-o sobre o problema.
- **Echo request/reply:** O comando `ping` envia uma mensagem ICMP Echo Request para um host de destino, se o host estiver acessível, ele responde com uma mensagem ICMP Echo Reply. Isso é comumente usado para testar a conectividade da rede e medir o tempo de ida e volta.
- **Transporte de mensagens:** As mensagens ICMP são encapsuladas dentro de datagramas IP. Isso significa que uma mensagem ICMP é a "carga útil" de um pacote IP.

---

### **Tabela de Mensagens ICMP**

| Tipo | Código | Descrição                  | Observações                                             |
| :--- | :----- | :------------------------- | :------------------------------------------------------ |
| 0    | 0      | **Echo Reply**             | Resposta ao comando `ping`.                             |
| 3    | 0      | **Network Unreachable**    | A rede de destino não pode ser alcançada.               |
| 3    | 1      | **Host Unreachable**       | O host de destino não pode ser alcançado.               |
| 3    | 2      | **Protocol Unreachable**   | Protocolo solicitado não disponível no host de destino. |
| 3    | 3      | **Port Unreachable**       | Porta solicitada não disponível no host de destino.     |
| 3    | 6      | **Dest Network Unknown**   | A rede de destino é desconhecida.                       |
| 3    | 7      | **Dest Host Unknown**      | O host de destino é desconhecido.                       |
| 4    | 0      | **Source Quench**          | Indicava congestionamento (pouco usado).                |
| 8    | 0      | **Echo Request**           | Usado pelo comando `ping` para testar a conectividade.  |
| 9    | 0      | **Router Advertisement**   | Roteadores anunciam sua presença.                       |
| 10   | 0      | **Router Solicitation**    | Hosts solicitam anúncios de roteador.                   |
| 11   | 0      | **TTL Expired in Transit** | O campo TTL do pacote atingiu zero.                     |
| 12   | 0      | **IP Header Bad**          | O cabeçalho IP contém um erro.                          |


Exportar para as Planilhas
Vamos ver alguns dos mais importantes:

- **Tipo 0, Código 0: echo reply (ping)**
    
    - Esta é a resposta a uma requisição ICMP Echo Request (ping). Indica que o host de destino recebeu a requisição e está enviando uma resposta.
- **Tipo 3 (Destination Unreachable - Destino Inacessível):** Este tipo é usado para indicar que um destino não pode ser alcançado. Os vários códigos especificam _por que_ ele está inalcançável:
    
    - **Código 0: dest. network unreachable** (Rede de destino inalcançável) - A rede onde o host de destino reside não pode ser alcançada.
    - **Código 1: dest. host unreachable** (Host de destino inalcançável) - O host específico não pode ser alcançado, mesmo que a rede seja alcançável.
    - **Código 2: dest. protocol unreachable** (Protocolo de destino inalcançável) - O host de destino é alcançável, mas o protocolo solicitado (por exemplo, TCP, UDP) não está disponível.
    - **Código 3: dest. port unreachable** (Porta de destino inalcançável) - O host de destino é alcançável, mas a porta específica para o serviço solicitado não está aberta ou disponível.
    - **Código 6: dest. network unknown** (Rede de destino desconhecida) - A rede não é conhecida pelo roteador.
    - **Código 7: dest. host unknown** (Host de destino desconhecido) - O host não é conhecido pelo roteador.
- **Tipo 4, Código 0: source quench (congestion control - not used)** (Supressão de Origem - controle de congestionamento - não usado)
    
    - Historicamente, esta mensagem era usada para controle de fluxo, sinalizando ao remetente para diminuir a velocidade devido ao congestionamento da rede. No entanto, é amplamente preterida e não é usada em redes modernas para controle de congestionamento.
- **Tipo 8, Código 0: echo request (ping)**
    
    - Esta é a mensagem enviada pelo utilitário `ping` para testar a conectividade.
- **Tipo 9, Código 0: route advertisement** (Anúncio de Rota)
    
    - Usado em mensagens de anúncio de roteador, onde os roteadores informam aos hosts sobre as rotas disponíveis.
- **Tipo 10, Código 0: router discovery** (Descoberta de Roteador)
    
    - Usado por hosts para descobrir roteadores em seu segmento de rede.
- **Tipo 11, Código 0: TTL expired** (Tempo de Vida expirado)
    
    - O campo "Time To Live" (Tempo de Vida) em um pacote IP evita que ele circule indefinidamente. Quando o TTL atinge zero, o roteador descarta o pacote e envia uma mensagem ICMP "TTL expired" de volta ao remetente. Isso é comumente visto quando um pacote está preso em um loop de roteamento ou o destino está muito distante.
- **Tipo 12, Código 0: bad IP header** (Cabeçalho IP inválido)
    
    - Indica que o cabeçalho IP do pacote recebido está malformado ou contém erros.

**4. Fluxograma Inferior:** Esta seção ilustra as categorias de mensagens ICMP, originando-se de um bloco "Erro reportado".

- **Destino inacessível:** Corresponde às mensagens "Tipo 3" na tabela.
- **Tráfego:** Isso pode representar amplamente mensagens relacionadas ao fluxo ou controle de rede, embora não seja um tipo ICMP específico. Poderia se referir a mensagens como Source Quench ou outras mensagens de controle que influenciam o tráfego.
- **Tempo Excedido:** Corresponde às mensagens "Tipo 11" (TTL expirado).
- **Problema nos parâmetros:** Corresponde a mensagens como "Tipo 12" (Cabeçalho IP inválido), indicando problemas com os parâmetros do pacote.
- **Redirecionamento:** Isso se refere a mensagens de Redirecionamento ICMP (não explicitamente mostradas na seleção da tabela, mas um tipo ICMP conhecido). Elas são enviadas por roteadores para hosts para informá-los sobre uma rota melhor para um determinado destino.