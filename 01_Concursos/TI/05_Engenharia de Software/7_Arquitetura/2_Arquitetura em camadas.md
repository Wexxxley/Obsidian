
#Concluded 

---

A ideia central é organizar as classes ou módulos em **camadas** dispostas de forma **hierárquica**. <mark style="background: #BBFABBA6;">Uma camada só pode usar os serviços (chamar métodos, instanciar objetos, etc.) da camada imediatamente inferior a ela. Ela não pode "pular" camadas nem acessar camadas superiores.</mark>

### Arquitetura em Três Camadas

1. **Interface com o Usuário (Camada de Apresentação):**
    - Responsável por **toda a interação** com o usuário.
    - Inclui a exibição de informações e o tratamento de entradas (cliques, digitação, etc.).        
    - Pode ser uma aplicação desktop (com interface gráfica) ou Web.
        
2. **Lógica de Negócio (Camada de Aplicação):**
    - Implementa as **regras de negócio** específicas do domínio do sistema.
    - Processa os dados recebidos da camada de interface e toma decisões com base nas regras.
        
3. **Banco de Dados (Camada de Dados/Persistência):**    
    - Responsável por **armazenar e recuperar** os dados manipulados pelo sistema.
        
![](../../../../attachments/Pasted%20image%2020251023202231.png)

**Distribuição Física (Típica):**
- A **Interface com o Usuário** executa na máquina do cliente.
- A **Lógica de Negócio** executa em um servidor dedicado (servidor de aplicação).     
- O **Banco de Dados** reside em seu próprio servidor.

**Observações:**
- A camada de aplicação pode ser subdividida internamente, por exemplo, um módulo de persistência para isolar a lógica de negócio dos detalhes do banco de dados.

- **Arquitetura em Duas Camadas:** É uma variação onde as camadas de Interface e Lógica de Negócio são unidas e executam no cliente, que acessa diretamente o Banco de Dados. A desvantagem é que exige mais poder de processamento nas máquinas clientes16.
