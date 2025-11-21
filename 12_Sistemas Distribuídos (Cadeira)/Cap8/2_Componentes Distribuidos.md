

---

O livro faz uma distinção importante: embora CORBA e RMI sejam poderosos, eles ainda tratam de _objetos_. O desenvolvedor ainda precisa escrever muito código de infraestrutura.

#### **1. O que é um Componente em Sistemas Distribuídos?**

Um componente é mais do que apenas um objeto. Ele é uma unidade de software que:
- É **autossuficiente** e implantável.
- Torna suas **dependências explícitas**.
- Não roda "solto" no sistema operacional; ele roda dentro de um **Container**.

#### **2. O Conceito de Container**

O componente (seu código de negócio) é "jogado" dentro de um Container (o servidor de aplicação). O Container atua como um "super-middleware". Ele envolve o componente e intercepta todas as chamadas que chegam e saem dele. Isso permite a **Programação Declarativa**:

- Em vez de escrever código para abrir uma transação de banco de dados, você apenas configura no Container: _"Este componente precisa de transação"_.
- O Container lê essa configuração e abre/fecha a transação automaticamente para você.
- O Container gerencia segurança, persistência, ciclo de vida e _pooling_ de threads automaticamente.

#### **3. Estudo de Caso: Enterprise JavaBeans (EJB)**

O **EJB** é a especificação padrão de componentes para o mundo Java (parte do Java EE / Jakarta EE). 

- **Session Beans:** Representam a lógica de negócio ou um processo.
    - Stateless: Como uma função pura. Não guarda dados de um cliente específico. 
    - _Stateful (Com Estado):_ Mantém uma conversação com o cliente (ex: um carrinho de compras).
        
- **Message-Driven Beans (MDBs):** Componentes desenhados para receber mensagens assíncronas (via filas JMS). Eles não respondem diretamente ao cliente, mas reagem a eventos.
    
- **Entity Beans (Beans de Entidade):** Representam os dados no banco de dados (uma linha na tabela "Cliente" vira um objeto "Cliente"). O Container cuida de salvar e carregar isso do banco automaticamente.

#### **4. Comparação: Objetos vs. Componentes**

- **Objetos (CORBA/RMI):** Foco na comunicação (RPC). O desenvolvedor cuida da infraestrutura.
- **Componentes (EJB):** Foco na implantação e configuração. O Container cuida da infraestrutura. O desenvolvimento é mais rápido, mas o servidor é mais pesado.