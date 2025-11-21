

---
#### **1. A Evolução: De Objetos para Componentes**

- **Objetos Distribuídos:** São unidades de encapsulamento que possuem estado e comportamento. Eles são acessados através de **interfaces** bem definidas. O principal objetivo aqui é a **interoperabilidade** — permitir que um objeto escrito em C++ interaja com um objeto escrito em Java como se fossem locais.
    
- **Componentes:** Um componente é uma unidade de software **implantável** e autossuficiente. Enquanto um objeto é uma unidade de _programação_ (código), um componente é uma unidade de _implantação_ (binário). Componentes geralmente vêm com "contratos" mais ricos, especificando não apenas o que eles fornecem, mas também o que eles precisam (dependências) para funcionar.    

---
#### **2. O Modelo de Objetos Distribuídos**

- **Referências de Objeto Remoto (ROR):** Como vimos no Cap. 5, outros objetos acessam um objeto distribuído através de uma referência remota. No entanto, neste capítulo, enfatiza-se que essa referência deve ser capaz de apontar para objetos em **qualquer lugar**, rodando em **qualquer sistema operacional** e escritos em **qualquer linguagem**.
    
- **Interfaces:** A interface é o contrato público. A importância de uma **Linguagem de Definição de Interface (IDL)** torna-se crítica. Ela define os métodos de forma neutra, independente da linguagem de implementação.
    
- **Ações:** Uma ação (como uma transação bancária) é iniciada por uma invocação de método, que pode resultar em uma cadeia de invocações através de vários objetos distribuídos em diferentes máquinas.
    
- **Exceções:** O modelo deve prever exceções ricas para lidar com falhas.
    
- **Coleta de Lixo:** Em sistemas complexos e heterogêneos, a coleta de lixo distribuída é essencial para liberar recursos de objetos que não são mais usados.

---
#### **3. O Papel do Middleware**

Para que esse modelo funcione na prática, precisamos de uma camada de software intermediária: o **Middleware de Objetos Distribuídos**.

O exemplo clássico é o **CORBA** (Common Object Request Broker Architecture). O papel desse middleware é fornecer um **Barramento de Objetos** ou **ORB (Object Request Broker)**.

- O ORB cuida de localizar o objeto remoto, ativar o servidor se necessário, transmitir os parâmetros (convertendo os formatos de dados entre diferentes linguagens/OS) e retornar o resultado.

---
### **4. Estudo de Caso - CORBA**

Diferente do RMI Java, o objetivo do CORBA é permitir que aplicações escritas em **diferentes linguagens** (C++, Java, Python, COBOL, etc.) e rodando em **diferentes plataformas** interajam entre si de forma transparente.
#### **1. A CORBA IDL (Linguagem de Definição de Interface)**

O coração do CORBA é a sua IDL. Como o CORBA precisa suportar muitas linguagens, ele não pode usar a sintaxe de interface do Java ou do C++. Ele usa sua própria linguagem neutra.

- **O Contrato:** O desenvolvedor define a interface do serviço usando a sintaxe IDL.
- **Mapeamento de Linguagem:** O padrão CORBA define regras precisas de como os tipos da IDL (ex: `long`, `string`, `struct`) são traduzidos para os tipos nativos de cada linguagem de programação.
- **Compilador IDL:** Uma ferramenta que lê o arquivo IDL e gera automaticamente o código fontena linguagem de destino escolhida pelo desenvolvedor.

#### **2. Arquitetura do CORBA**

A arquitetura do CORBA é projetada para desacoplar o cliente da implementação do servidor.
![](../../attachments/Pasted%20image%2020251121185916.png)

- **ORB (Object Request Broker):** É a biblioteca de middleware que deve estar presente tanto no cliente quanto no servidor. Sua função é localizar o objeto, transmitir a requisição e devolver a resposta.
- **Stub do Cliente (Proxy Estático):** Código gerado pelo compilador IDL que roda no cliente. Ele expõe a interface do servidor na linguagem nativa do cliente.
    
- **Skeleton do Servidor:** Código gerado pelo compilador IDL que roda no servidor. Ele recebe a requisição do ORB, desempacota os parâmetros e chama o método real no objeto de implementação.
    
- **Adaptador de Objeto (Object Adapter - POA):** Este é um componente crucial que fica entre o ORB e o objeto de implementação (o servo).
    
    - Ele gerencia o ciclo de vida dos objetos servidores.
        
    - Ele mapeia as referências de objeto remoto para as instâncias reais das classes (servos).
        
    - Ele permite ativar servidores sob demanda.
        

#### **3. Invocação Dinâmica vs. Estática**

O livro destaca que o CORBA oferece duas formas de invocação:

1. **Invocação Estática (via Stubs):** O cliente precisa ter o código do stub compilado junto com ele (o jeito tradicional). É mais rápido e verificável em tempo de compilação.
    
2. **Invocação Dinâmica (DII - Dynamic Invocation Interface):** O cliente pode descobrir interfaces em tempo de execução (usando um Repositório de Interfaces) e construir requisições dinamicamente, sem ter os stubs compilados. É mais flexível, mas mais complexo e lento.
    

#### **4. Protocolo de Interoperabilidade (GIOP/IIOP)**

Para garantir que um ORB de um fabricante (ex: ORB da IBM em Java) converse com um ORB de outro fabricante (ex: ORB da IONA em C++), o CORBA define o **GIOP (General Inter-ORB Protocol)**.

A implementação mais famosa do GIOP sobre a Internet (TCP/IP) é chamada de **IIOP (Internet Inter-ORB Protocol)**. É graças ao IIOP que a interoperabilidade real acontece na rede.

#### **5. Serviços CORBA**

O CORBA não define apenas como enviar mensagens (RPC), mas especifica um conjunto rico de **Serviços Horizontais** que expandem as capacidades do sistema distribuído:

- **Serviço de Nomes (Naming Service):** Um diretório hierárquico (como um sistema de arquivos) para encontrar referências de objetos pelo nome.
    
- **Serviço de Negociação (Trading Service):** Permite encontrar objetos com base em suas _características_ ou capacidades (ex: "preciso de uma impressora colorida no 3º andar"), e não apenas pelo nome.
    
- **Serviço de Eventos e Notificações:** Para comunicação assíncrona publicar-assinar.
    
- **Serviço de Transações e Segurança.**