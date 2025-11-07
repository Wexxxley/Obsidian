
#Concluded 

---
Esta seção apresenta o **RMI Java** como uma implementação específica do modelo de RMI, mas com a particularidade de ser um sistema de **linguagem única** (Java para Java). 

---
### **1. Interfaces Remotas em Java**

Para definir um objeto como remoto, o programador cria uma **interface que extends** a interface **java.rmi.Remote**. Um requisito fundamental é que todos os métodos nessa interface devem declarar que disparam a exceção **RemoteException**. Isso força o programador a lidar com as falhas de rede, tornando a natureza distribuída explícita.
### **2. Passagem de Parâmetros**

A RMI Java usa a **serialização de objetos** para empacotar argumentos e resultados. O comportamento da passagem de parâmetros depende do tipo do objeto:
    
1. **Objetos Remotos**: Se um argumento ou resultado é um objeto que implementa a interface Remote, ele é passado **por referência**. O receptor pode então fazer chamadas remotas de volta para esse objeto.

2. **Objetos Não Remoto**: Se um objeto não implementa `Remote` mas implementa `java.io.Serializable`, ele é passado **por valor**. O objeto é serializado, uma cópia completa dele é enviada pela rede, e um novo objeto é recriado no processo de destino.
        
- **Exemplo `ShapeList`**:

    - A interface `Shape` é definida como `Remote`, de modo que cada figura no quadro branco é um objeto remoto individual.
    - A classe `GraphicalObject` (que contém os dados da figura, como cor e posição) é definida como `Serializable`.
    - O método `newShape(GraphicalObject g)` passa o objeto `g` **por valor** (uma cópia dos dados é enviada).
    - O método retorna um objeto `Shape` (que é `Remote`), significando que ele retorna uma **referência** para o novo objeto `Shape` criado no servidor.

- **Download Dinâmico de Classes**:
    - Quando um processo recebe uma referência de objeto remoto para uma classe que ele nunca viu antes, ele pode baixar automaticamente a classe do **proxy (stub)** correspondente de um local de rede (geralmente um servidor Web).
        
    - Da mesma forma, quando recebe um objeto passado por valor (serializado), ele pode baixar dinamicamente a classe desse objeto se não a possuir localmente.
        
    - Isso permite que o sistema seja estendido dinamicamente (por exemplo, adicionando novos tipos de `Shape` ao quadro branco) sem precisar atualizar todos os clientes8.


- **RMIregistry**: É o binder do RMI Java. É um serviço simples de nomes que roda em um servidor e mantém um mapa de nomes textuais para referências de objetos remotos. Um servidor usa o RMIregistry para registrar seus objetos remotos com um nome, e os clientes o usam para procurar esses objetos pelo nome.
    
- **Reflexão**: Em vez de exigir que o programador gere um "esqueleto" estático para o servidor (como na RPC), o RMI usa um **despachante genérico**. Esse despachante recebe a requisição, usa a reflexão para descobrir qual método deve ser chamado no servente, desempacota os argumentos e invoca o método. Isso simplifica muito o desenvolvimento, pois o programador não precisa mais da etapa de compilação do esqueleto.
