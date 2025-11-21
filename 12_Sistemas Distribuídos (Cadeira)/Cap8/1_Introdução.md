

---
#### **1. A Evolução: De Objetos para Componentes**

- **Objetos Distribuídos:** São unidades de encapsulamento que possuem estado e comportamento. Eles são acessados através de **interfaces** bem definidas. O principal objetivo aqui é a **interoperabilidade** — permitir que um objeto escrito em C++ interaja com um objeto escrito em Java como se fossem locais.
    
- **Componentes:** Um componente é uma unidade de software **implantável** e autossuficiente. Enquanto um objeto é uma unidade de _programação_ (código), um componente é uma unidade de _implantação_ (binário). Componentes geralmente vêm com "contratos" mais ricos, especificando não apenas o que eles fornecem, mas também o que eles precisam (dependências) para funcionar.    

#### **2. O Modelo de Objetos Distribuídos**

- **Referências de Objeto Remoto (ROR):** Como vimos no Cap. 5, outros objetos acessam um objeto distribuído através de uma referência remota. No entanto, neste capítulo, enfatiza-se que essa referência deve ser capaz de apontar para objetos em **qualquer lugar**, rodando em **qualquer sistema operacional** e escritos em **qualquer linguagem**.
    
- **Interfaces:** A interface é o contrato público. A importância de uma **Linguagem de Definição de Interface (IDL)** torna-se crítica. A IDL é a "cola" que permite a interoperabilidade. Ela define os métodos de forma neutra, independente da linguagem de implementação.
    
- **Ações:** Uma ação (como uma transação bancária) é iniciada por uma invocação de método, que pode resultar em uma cadeia de invocações através de vários objetos distribuídos em diferentes máquinas.
    
- **Exceções:** O modelo deve prever exceções ricas para lidar com falhas parciais, timeouts e problemas de rede.
    
- **Coleta de Lixo:** Em sistemas complexos e heterogêneos, a coleta de lixo distribuída (como contagem de referências ou leasing) é essencial para liberar recursos de objetos que não são mais usados.
    

#### **3. O Papel do Middleware**

Para que esse modelo funcione na prática, precisamos de uma camada de software intermediária: o **Middleware de Objetos Distribuídos**.

O exemplo clássico e mais detalhado que o livro usará é o **CORBA** (Common Object Request Broker Architecture). O papel desse middleware é fornecer um **Barramento de Objetos (Object Bus)** ou **ORB (Object Request Broker)**.

- Imagine um "tubo" universal onde qualquer objeto pode se conectar.
    
- O ORB cuida de localizar o objeto remoto, ativar o servidor se necessário, transmitir os parâmetros (convertendo os formatos de dados entre diferentes linguagens/OS) e retornar o resultado.