

---

O livro define o Docker como uma plataforma para executar aplicações em unidades leves chamadas contêineres. O texto destaca que essa tecnologia se tornou onipresente, sendo utilizada desde funções serverless na nuvem até planejamentos estratégicos em grandes empresas1.

O autor ressalta que o Docker é uma competência essencial (_core competency_) para operadores e desenvolvedores. Pesquisas do Stack Overflow desde 2019 mostram o Docker consistentemente como a tecnologia mais desejada ou amada pelos profissionais2.

Estrutura de aprendizado

Apesar de ser uma tecnologia fundamental, o Docker é descrito como simples de aprender. O livro propõe um caminho prático:

- **Capítulo 2:** Execução de contêineres.
    
- Capítulo 3: Empacotamento de aplicações.
    
    Os capítulos subsequentes focam em tarefas práticas e laboratórios que funcionam em qualquer sistema operacional (Windows, Mac e Linux)3.
    

A experiência do autor e o problema da "Passagem de Bastão"

O autor compartilha um estudo de caso técnico de 2014, envolvendo um projeto de APIs para dispositivos Android. Inicialmente, o Docker foi usado apenas para ferramentas de desenvolvimento e servidores de build, mas evoluiu para rodar as APIs em ambientes de teste e, finalmente, em produção, atendendo a requisitos estritos de disponibilidade e escala4.

O ponto crítico técnico abordado aqui é a **centralização do toolchain** (cadeia de ferramentas).

- **Antes do Docker:** A transferência do projeto para uma nova equipe levava duas semanas. Desenvolvedores precisavam instalar versões específicas de diversas ferramentas, e administradores precisavam configurar outras ferramentas diferentes nos servidores.
    
- **Com Docker:** A transferência foi reduzida a um único arquivo `README`. O único requisito para construir, implantar e gerenciar a aplicação, tanto localmente quanto no cluster de produção, passou a ser o Docker. Isso eliminou a complexidade de configuração de ambiente5.
    

---

### **1.1.1 Migração de aplicações para a nuvem (Páginas 4, 5 e 6)**

O livro analisa tecnicamente as opções de migração para a nuvem, contrastando métodos tradicionais com a abordagem via contêineres.

As abordagens tradicionais (IaaS vs. PaaS)

Antes do Docker, havia um compromisso técnico difícil entre duas opções, ilustradas na Figura 1.1 6666:

1. **IaaS (Infrastructure as a Service):**
    
    - **Funcionamento:** Você cria uma Máquina Virtual (VM) para cada componente da aplicação.
        
    - **Vantagem:** Portabilidade entre nuvens.
        
    - **Desvantagem técnica:** Alto custo operacional e de execução, pois as VMs tendem a ser subutilizadas.
        
2. **PaaS (Platform as a Service):**
    
    - **Funcionamento:** Mapeia-se cada componente da aplicação para um serviço gerenciado do provedor de nuvem.
        
    - **Vantagem:** Menor custo de execução e facilidade de gerenciamento.
        
    - **Desvantagem técnica:** _Lock-in_ (aprisionamento) em uma nuvem específica e a complexidade de migrar o projeto para os serviços proprietários.
        

A abordagem Docker (A terceira opção)

O Docker oferece uma alternativa que remove esses compromissos. A estratégia consiste em migrar cada parte da aplicação para um contêiner.

- **Resultado:** A aplicação pode ser executada em serviços de Kubernetes gerenciados (como AKS ou Amazon ECS) ou em data centers próprios.
    
- **Benefício Técnico:** Combina a portabilidade do IaaS com a eficiência de recursos do PaaS.
    

A **Figura 1.2** ilustra essa arquitetura: os componentes rodam isolados como em VMs, mas são leves e eficientes. O resultado é uma aplicação portátil que roda com baixo custo em qualquer nuvem ou laptop sem alterações de código 7777.

Esforço de Migração

O autor detalha que essa migração exige investimento na criação de Dockerfiles (scripts de instalação) e manifestos de aplicação (Docker Compose ou Kubernetes), mas enfatiza que não é necessário alterar o código da aplicação. O resultado final utiliza a mesma stack tecnológica em todos os ambientes8.

---

### **1.1.2 Modernização de aplicações legadas (Páginas 6 e 7)**

Esta seção aborda como o Docker auxilia na evolução de arquiteturas monolíticas sem a necessidade de reescritas completas imediatas.

O problema dos Monólitos

Embora monólitos rodem em contêineres, eles limitam a agilidade. O autor compara o deploy automatizado de 30 segundos de um contêiner moderno com o ciclo de testes de regressão de duas semanas necessário para um monólito de 2 milhões de linhas de código9.

Estratégia de decomposição

O Docker permite modernizar a arquitetura adotando novos padrões gradualmente:

1. Move-se a aplicação legada para um contêiner (criando um "monólito em um contêiner").
    
2. Utiliza-se a rede virtual do Docker para comunicação interna.
    
3. Novas funcionalidades são desenvolvidas em contêineres separados, quebrando o monólito aos poucos.
    

A **Figura 1.3** detalha tecnicamente essa arquitetura distribuída 10:

- O monólito original roda em um contêiner sem alterações de código.
    
- Um componente de roteamento direciona requisições externas para o monólito ou para novos contêineres, dependendo da rota solicitada.
    
- Novas _features_ são isoladas em seus próprios contêineres, permitindo ciclos de lançamento independentes e o uso de stacks tecnológicas diferentes das do monólito.
    

Benefícios Técnicos

Essa abordagem oferece benefícios de microsserviços (agilidade, escalabilidade, isolamento de falhas) sem parar o desenvolvimento para uma reescrita total do software, permitindo entregar uma aplicação mais resiliente em estágios 11.

---

Isso cobre detalhadamente o conteúdo técnico e as figuras das páginas 4 a 7 fornecidas no seu texto.

**Diga "next" para eu continuar a explicação das páginas seguintes (Cloud-native apps, Serverless e DevOps).**