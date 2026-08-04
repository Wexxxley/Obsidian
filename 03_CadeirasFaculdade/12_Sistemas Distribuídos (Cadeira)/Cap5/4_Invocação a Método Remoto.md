


---
Invocação a Método Remoto (RMI) é a evolução da RPC para o POO. O conceito central é o mesmo da RPC: um objeto em um processo pode invocar um método em um objeto que está em outro processo (remoto), e o middleware de RMI oculta a complexidade da comunicação.

A RMI compartilha muitas características com a RPC: ambas suportam programação com interfaces, são construídas sobre protocolos de requisição-resposta e oferecem transparência.

No entanto, a RMI introduz duas diferenças fundamentais e poderosas:

1. <mark style="background: #ADCCFFA6;">Permite o uso de princípios de POO</mark> (encapsulamento, herança de interface) no desenvolvimento de sistemas distribuídos.
    
2. <mark style="background: #ADCCFFA6;">Permite que referências de objeto remoto sejam passadas como argumentos</mark> e resultados em invocações de métodos, algo que a RPC  não pode fazer.    

---
### **1. Questões de Projeto para RMI**

- **Objetos Remotos:** São objetos que podem receber invocações remotas. Outros objetos só podem invocar os métodos de um objeto remoto se tiverem acesso à sua referência de objeto remoto.
    
- **Interfaces Remotas:** Cada objeto remoto implementa uma interface remota, que especifica quais de seus métodos podem ser invocados remotamente. Clientes e servidores se comunicam apenas através dessas interfaces.
    
- **Exceções Distribuídas:** Uma invocação remota pode falhar por motivos que não existem em uma chamada local (falha de rede, colapso do servidor). Portanto,  interfaces remotas devem declarar que podem disparar exceções específicas de distribuição (como RemoteException).
    
- **Coleta de Lixo Distribuída:** O sistema deve garantir que um objeto remoto continue a existir enquanto qualquer referência (local ou remota) a ele existir em qualquer lugar do sistema distribuído.

---
### 2. **Implementação de RMI**

Assim como a RPC, a RMI é implementada usando componentes de software que automatizam a comunicação.

![](../../../attachments/Pasted%20image%2020251107142504.png)

- **proxy/Stub do Cliente:** Um objeto no lado do cliente que age como um representante local para o objeto remoto. Ele implementa a mesma interface remota que o objeto real. Quando o cliente chama um método no proxy, o proxy empacota os argumentos em uma mensagem de requisição e a envia pela rede.
    
- **Esqueleto**: Um objeto no lado do servidor que recebe a mensagem de requisição. Ele desempacota os argumentos e invoca o método correspondente no objeto de implementação real.
    
- **Servente:** É a instância da classe no servidor que contém a lógica de negócios real e implementa os métodos da interface remota
    
- **Módulo de Referência Remota:** Um componente em cada processo que gerencia a tradução entre referências de objetos locais (para proxies ou serventes) e as **referências de objeto remoto** (identificadores globalmente únicos) que são transmitidas pela rede.

O livro também menciona outros conceitos de implementação:

- **Binder:** Um serviço separado que atua como uma lista telefônica, permitindo que os clientes procurem um objeto remoto usando um nome textual (ex: "ServiçoDeImpressora") para obter sua referência de objeto remoto inicial.
    
- **Ativação:** Um mecanismo que permite que objetos fiquem em estado "passivo" (armazenados em disco) e sejam ativados (carregados na memória) sob demanda quando uma invocação para eles chega. Isso economiza recursos, pois o servidor não precisa manter todos os seus objetos na memória o tempo todo.

---
### **3. Coleta de Lixo Distribuída**

Como os objetos remotos são passados por referência, o sistema precisa de uma forma de saber quando um objeto remoto não é mais necessário e pode ser excluído.

- A RMI Java usa um algoritmo de contagem de referência. O servidor mantém um registro de quais clientes possuem uma referência para seu objeto.
- Quando um cliente cria um proxy, ele chama `addRef()` no servidor.
- Quando o coletor de lixo local do cliente determina que o proxy não é mais usado, ele chama `removeRef()` no servidor.    
- **Leasing:** Para lidar com falhas de clientes (que podem falhar antes de chamar `removeRef()`), o servidor concede "arrendamentos"  de curta duração para as referências. O cliente deve renovar periodicamente o arrendamento. Se um cliente falhar, seu arrendamento expirará, e o servidor removerá a referência automaticamente.
