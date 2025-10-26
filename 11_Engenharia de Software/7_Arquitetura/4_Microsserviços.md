
#Concluded 

---
### **Sistemas Monolíticos**

Tradicionalmente, muitos sistemas eram construídos como uma única unidade coesa. <mark style="background: #ADCCFFA6;">Nesse modelo, todas as funcionalidades (interface do usuário, lógica de negócio, acesso a dados) são empacotadas e implantadas juntas.</mark>

**Desvantagens dos Monolitos:**
    - **Dificuldade de Manutenção e Evolução:** Uma pequena alteração em uma parte do sistema pode exigir a recompilação e reimplantação de todo o sistema. 
    - **Barreira Tecnológica:** É difícil adotar novas tecnologias ou linguagens, pois todo o sistema está acoplado a uma única pilha tecnológica.
    - **Fragilidade:** Uma falha em um componente pode derrubar a aplicação inteira.
    - **Tempo de Implantação:** O processo de build, teste e implantação do monolito inteiro pode ser demorado.

---
### **Microsserviços:**

Em contraste com os monolitos, <mark style="background: #ADCCFFA6;">a arquitetura de microsserviços estrutura uma aplicação como uma coleção de pequenos serviços independentes.</mark>

**Características Principais:**
- **Pequenos e Focados:** Cada serviço é responsável por uma capacidade de negócio específica (ex: serviço de autenticação, serviço de catálogo de produtos, serviço de carrinho de compras).
- **Independentemente Implantáveis:** Cada serviço pode ser desenvolvido, testado, implantado e escalado de forma independente dos outros.
- **Tecnologia Diversificada:** Cada serviço pode ser implementado usando a tecnologia (linguagem, banco de dados) mais adequada para sua função específica.
- **Descentralização:** Cada serviço pode ter seu próprio banco de dados e a governançatende a ser descentralizada entre as equipes responsáveis por cada serviço.

**Benefícios dos Microsserviços:**
- **Maior Agilidade:** Equipes podem desenvolver, testar e implantar seus serviços de forma independente e mais rápida.
- **Melhor Escalabilidade:** É possível escalar apenas os serviços que realmente precisam, otimizando o uso de recursos.
- **Resiliência:** A falha em um serviço não necessariamente derruba toda a aplicação (se projetado corretamente com tolerância a falhas).
- **Flexibilidade Tecnológica:** Permite usar a melhor tecnologia para cada tarefa e facilita a adoção de novas tecnologias.

**Desafios dos Microsserviços:**
- **Complexidade Operacional:** Gerenciar múltiplos serviços implantados, monitorá-los e garantir a comunicação entre eles é mais complexo do que gerenciar um único monolito.
- **Complexidade Distribuída:** Lidar com comunicação de rede (latência, falhas), consistência de dados entre serviços e transações distribuídas introduz novos desafios.
- **Testes:** Testar as interações entre múltiplos serviços (testes de integração/ponta-a-ponta) é mais complexo.
- **Overhead de Rede:** A comunicação constante entre serviços via rede pode introduzir latência.
- **Gerenciamento de Dados:** Cada serviço tendo seu próprio banco de dados pode dificultar consultas que abrangem dados de múltiplos serviços e garantir a consistência geral.

---
### GRPC
É um sistema moderno de **Chamada Remota de Procedimentos** (RPC - Remote Procedure Call). Sua principal função é **viabilizar a comunicação** entre diferentes aplicações ou serviços, especialmente em arquiteturas distribuídas como microsserviços.

![](attachments/Pasted%20image%2020251026161835.png)

**Como Funciona**:
- Baseia-se no conceito de RPC, onde uma aplicação (cliente) pode chamar um método ou procedimento em outra aplicação (servidor) que está rodando em um processo diferente, possivelmente em outra máquina, como se fosse uma chamada local.
  - Inclui uma **Linguagem de Definição de Interfaces** (IDL - Interface Definition Language), como o _Protocol Buffers_ (proto3, no exemplo)7.
        
3. **Linguagem de Definição de Interfaces (IDL)**8:
    
    - Com essa linguagem, você define a "forma" do serviço:
        
        - Define o **Serviço** em si (ex: `ShippingService`)9.
            
        - Define as **Operações** ou métodos que o serviço oferece (ex: `rpc GetShippingRate`)10.
            
        - Define a estrutura das **mensagens de entrada** (payload/request, ex: `ShippingPayload` com um campo `cep`) e **mensagens de saída** (response, ex: `ShippingResponse` com um campo `value`) para cada operação11.
            
    - A partir dessa definição, ferramentas gRPC podem gerar código base (stubs) para clientes e servidores em diversas linguagens de programação.
        
    - O **Cliente** usa o stub gerado para chamar os métodos remotos como se fossem locais1212.
        
    - O **Servidor** implementa a lógica real dos métodos definidos na interface131313.
        
4. **Exemplo de Arquitetura**14:
    
    - As imagens mostram uma arquitetura comum onde:
        
        - A **Interface do Usuário (UI / Front-end)** se comunica com um **Controller** (ou API Gateway/Backend-for-Frontend) usando **REST**15.
            
        - O **Controller**, por sua vez, se comunica com serviços de backend (como `Shipping Service` e `Inventory Service`) usando **gRPC**16.
            
    - Isso ilustra que gRPC é frequentemente usado para a comunicação interna e eficiente entre microsserviços no backend, enquanto a comunicação com o front-end pode continuar sendo REST.
        
    - A Imagem 3 mostra exemplos de código:
        
        - No **Servidor** (Shipping Service), como o método `GetShippingRate` é implementado17.
            
        - No **Controller** (Cliente gRPC), como ele recebe uma requisição REST (`app.get('/shipping/:cep', ...)`), extrai o parâmetro (`cep`) e chama o método gRPC `GetShippingRate` no serviço remoto (`shipping.GetShippingRate(...)`)18.

![](attachments/Pasted%20image%2020251026161855.png)

Em resumo, gRPC é um framework de RPC de alto desempenho, ideal para comunicação entre serviços (microsserviços), que usa definição de interfaces fortemente tipadas (como Protocol Buffers) e um protocolo binário eficiente.