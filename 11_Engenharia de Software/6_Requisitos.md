

---
### **1. O que são requisitos e tipos**
**Requisitos definem o que um sistema deve fazer e sob quais restrições ele deve operar**. A definição de requisitos é uma etapa crucial no desenvolvimento de software, pois de nada adianta ter um sistema bem projetado se ele não atende às necessidades dos usuários. Problemas na especificação de requisitos podem gerar custos altos de retrabalho ou, no limite, levar à rejeição do sistema pelos clientes.

Os requisitos são divididos em duas categorias principais:

• **Requisitos Funcionais**: Definem **o que o sistema deve fazer**, ou seja, suas funcionalidades e serviços. Por exemplo, em um sistema de _home-banking_, os requisitos funcionais incluem informar saldo, realizar transferências, pagar boletos, etc..

• **Requisitos Não-Funcionais**: Definem **como o sistema deve operar**, ou seja, as restrições e a qualidade de serviço esperada. Eles incluem características como desempenho, disponibilidade, segurança, privacidade, usabilidade, entre outras. Diferente dos funcionais, os requisitos não-funcionais devem ser especificados de forma quantitativa, usando métricas. Por exemplo, em vez de dizer "o sistema deve ser rápido", é melhor especificar "99% das transações devem ter um tempo de resposta máximo de 1 segundo".

Além disso, os requisitos podem ser classificados como **requisitos de usuário** (descrições de alto nível na linguagem do cliente) e **requisitos de sistema** (descrições técnicas e detalhadas feitas pelos desenvolvedores).

---
### **2. Engenharia de Requisitos**

**Engenharia de Requisitos é o conjunto de atividades sistemáticas para descobrir, analisar, especificar e manter os requisitos de um sistema**. As principais atividades são:

• **Elicitação de Requisitos**: É o processo de descobrir os requisitos através da interação com os _stakeholders_. As técnicas para isso incluem entrevistas e questionários nos quais o desenvolvedor se integra ao ambiente de trabalho do cliente para observar suas atividades.

• **Documentação**: Em métodos ágeis, a documentação é simplificada (com Histórias de Usuário).

• **Verificação e Validação**: Os requisitos devem ser corretos, precisos (sem ambiguidade), completos, consistentes e verificáveis (testáveis).

• **Priorização**: Nem todos os requisitos especificados serão implementados nas primeiras versões do sistema, devido a restrições de prazo e custo.

Histórias de Usuário

Documentos de requisitos tradicionais, como os usados no modelo Waterfall, costumam ter centenas de páginas e podem levar mais de um ano para ficarem prontos. No entanto, eles apresentam alguns problemas crônicos:

1. **Ficam obsoletos rapidamente**, pois os requisitos mudam durante o desenvolvimento e as alterações não são propagadas para a documentação.

2. **São ambíguos e incompletos**, o que exige que os desenvolvedores voltem a conversar com os clientes para tirar dúvidas.

3. **Aumentam o risco do projeto**, pois se não houver conversas intermediárias, o cliente pode, ao final do desenvolvimento, concluir que aquele não é mais o sistema de que precisa, pois suas prioridades ou negócio mudaram.

Devido a esses problemas, uma longa fase inicial de especificação de requisitos é cada vez mais rara, especialmente em sistemas comerciais.

Os profissionais que propuseram os métodos ágeis perceberam esses problemas e criaram uma técnica pragmática chamada **Histórias de Usuário**. A ideia é substituir a extensa documentação escrita por uma comunicação verbal e frequente entre desenvolvedores e clientes.

A Fórmula 3 C's de uma História de Usuário

Uma história de usuário, conforme sugerido por Ron Jeffries, é composta por três partes (iniciadas pela letra "C"):

1. **Cartão (****Card****)**: É um documento físico, geralmente um cartão de papel, onde o cliente escreve, em poucas sentenças e com sua própria linguagem, uma funcionalidade que espera ver no sistema. A história no cartão funciona como um **lembrete** para conversas futuras.

2. **Conversas (****Conversations****)**: São as interações entre clientes e desenvolvedores, nas quais os clientes detalham e explicam o que foi escrito no cartão. Essa comunicação é fundamental, pois substitui a necessidade de especificações textuais completas e detalhadas. É por isso que métodos ágeis recomendam a presença de um representante dos clientes em tempo integral na equipe de desenvolvimento.

3. **Confirmação (****Confirmation****)**: São os **testes de aceitação**, também especificados pelo cliente, para verificar se a história foi implementada conforme o esperado. Eles descrevem os cenários e casos de teste que serão usados para confirmar a implementação e devem ser escritos o quanto antes, de preferência no início da iteração.

Dessa forma, a Engenharia de Requisitos ocorre ao longo de todo o desenvolvimento, com conversas diárias e um foco em colaboração, alinhando-se aos princípios do Manifesto Ágil.

Características de uma Boa História (INVEST)

Boas histórias de usuário devem seguir o acrônimo **INVEST**:

• **Independentes (****Independent****)**: Devem poder ser implementadas em qualquer ordem, sem dependências entre elas.

• **Negociáveis (****Negotiable****)**: O cartão é um "convite para conversas", onde clientes e desenvolvedores devem estar abertos a ceder e negociar os detalhes da implementação.

• **Valiosas (****Valuable****)**: Devem agregar valor ao negócio do cliente. Histórias puramente técnicas, como "o sistema deve usar React no front-end", não são escritas pelos clientes.

• **Estimáveis (****Estimable****)**: Os desenvolvedores devem conseguir estimar o esforço necessário para implementá-las.

• **Sucintas (****Small****)**: Histórias que serão implementadas em breve devem ser pequenas o suficiente para serem concluídas em poucos dias. Histórias maiores, conhecidas como **épicos**, ficam no final do _backlog_.

• **Testáveis (****Testable****)**: Devem ter critérios de aceitação objetivos e claros. Um contra-exemplo seria "o cliente não deve esperar muito", que é uma história vaga.

Antes de começar a escrever as histórias, recomenda-se listar os papéis dos principais usuários (_user roles_) do sistema, para evitar que os requisitos atendam apenas a um grupo específico. As histórias costumam seguir o formato: "Como um [papel de usuário], eu gostaria de [realizar algo com o sistema]".


Exemplos para "Usuário Típico"

Qualquer usuário da biblioteca pode realizar as operações descritas nestas histórias. Elas são resumidas e não entram em detalhes de implementação, que seriam definidos em conversas posteriores com a equipe de desenvolvimento.

• Como usuário típico, eu gostaria de **realizar empréstimos de livros**.

• Como usuário típico, eu gostaria de **devolver um livro** que tomei emprestado.

• Como usuário típico, eu gostaria de **renovar empréstimos** de livros.

• Como usuário típico, eu gostaria de **pesquisar por livros**.

• Como usuário típico, eu gostaria de **reservar livros** que estão emprestados.

• Como usuário típico, eu gostaria de **receber e-mails com novas aquisições**.

Exemplos para "Professor"

Estas histórias foram requisitadas especificamente por professores, possivelmente durante um workshop de escrita de histórias. No entanto, algumas funcionalidades, como a de doar livros, poderiam ser estendidas a outros usuários durante a fase de detalhamento.

• Como professor, eu gostaria de realizar **empréstimos de maior duração**.

• Como professor, eu gostaria de **sugerir a compra de livros**.

• Como professor, eu gostaria de **doar livros para a biblioteca**.

• Como professor, eu gostaria de **devolver livros em outras bibliotecas**.

    ◦ _Nota: Esta última história pode ser considerada um_ **"épico"**_, ou seja, uma história maior e mais complexa, pois exigiria a integração entre os sistemas de diferentes bibliotecas da universidade_.

Exemplos para "Funcionário da Biblioteca"

Estas histórias estão relacionadas às tarefas de organização e gerenciamento da biblioteca.

• Como funcionário da biblioteca, eu gostaria de **cadastrar novos usuários**.

• Como funcionário da biblioteca, eu gostaria de **cadastrar novos livros**.

• Como funcionário da biblioteca, eu gostaria de **dar baixa em livros estragados**.

• Como funcionário da biblioteca, eu gostaria de **obter estatísticas sobre o acervo**.

• Como funcionário da biblioteca, eu gostaria que o sistema **envie e-mails de cobrança** para alunos com empréstimos atrasados.

• Como funcionário da biblioteca, eu gostaria que o sistema **aplique multas** quando da devolução de empréstimos atrasados.