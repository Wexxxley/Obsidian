
---

Um dos problemas ao lidarmos com uma aplicação web é a necessidade de estarmos sempre disponíveis para responder a requisições enviadas pelos clientes. Quando recebemos uma requisição, normalmente precisamos processá-la: validar, conectar ao banco de dados, realizar algumas operações e, finalmente, retornar o recurso solicitado.

Em um cenário síncrono, enquanto processamos uma requisição, não conseguimos processar outra até que a primeira seja concluída. Esse fluxo de execução é chamado de blobueante, pois a aplicação fica "parada", aguardando a resposta de sistemas externos. Esse tempo de espera é conhecido como **bloqueio por I/O (Input/Output)** 

---
### Uvicorn não é bloqueante
Quando dizemos que a aplicação está bloqueada, estamos nos referindo somente ao código explícito da aplicação. O servidor de aplicação, em nosso caso o [`uvicorn`](https://fastapidozero.dunossauro.com/estavel/01/#uvicorn), já trabalha de forma não bloqueante. Ele cria uma fila de requisições e vai passando uma a uma à nossa aplicação conforme as respostas forem sendo retornadas.

Além disso, ele pode inicializar diversas cópias da nossa aplicação (mesmo síncronas) em um formato de workers e executar diversos processos para nossa aplicação. Se quisermos inicializar o uvicorn nesse modo, a única alteração necessária seria adicionar a flag `--workers <int>`. Algo como:

![[Pasted image 20250626183431.png]]
Uvicorn:
- O Uvicorn é o software que recebe as requisições HTTP dos clientes. Ele atua como uma interface entre a internet e sua aplicação Python.
- **Assíncrono:** Ele é construído para lidar com múltiplas requisições concorrentemente, sem bloquear o processo principal. Isso é crucial para aplicações de alta performance que fazem muitas operações de I/O (espera por respostas de bancos de dados, APIs externas, etc.). Ele usa o conceito de _event loop_ para gerenciar essas operações.
    
- **Para Python:** É escrito em Python e otimizado para rodar aplicações Python que seguem a especificação ASGI.
    

### Como o Uvicorn se encaixa com o FastAPI?

FastAPI é um framework web **ASGI**. Ele não tem um servidor web embutido para produção (embora você possa rodá-lo com `uvicorn main:app --reload` durante o desenvolvimento, o Uvicorn é o servidor que está por trás).

Quando você desenvolve uma API com FastAPI, você está construindo a "APP" (como na sua imagem). O Uvicorn é quem pega as requisições que chegam dos seus "Clientes" e as envia para o seu código FastAPI para processamento. Uma vez que o FastAPI processa a requisição e gera uma resposta, o Uvicorn a pega e a envia de volta para o cliente.

Quando você executa o comando `uvicorn main:app --reload`, você está _iniciando_ o software Uvicorn nessa máquina.
### Por que o Uvicorn na sua arquitetura?

Na sua imagem, o Uvicorn é o **gateway principal** para sua aplicação web.

- **Cliente_1, Cliente_2, Cliente_3:** Representam usuários, navegadores, aplicativos móveis ou outros serviços que estão enviando requisições HTTP para sua API.
    
- **Uvicorn:** Recebe essas requisições.
    
- **APP:** É a sua aplicação FastAPI (ou Starlette, etc.), onde está a lógica de negócio, as rotas que você definiu (como `/professor/create`). O Uvicorn encaminha as requisições para a APP processar.
    
- **Backlog:** Isso é interessante. Não é um componente padrão de um servidor web como o Uvicorn. Vamos explicar o que é um backlog a seguir, e como ele pode se relacionar com isso.
    

**Em resumo, o Uvicorn é o motor que permite que sua aplicação FastAPI receba e responda a requisições HTTP de forma rápida e eficiente, especialmente em cenários de alta concorrência, tirando proveito da programação assíncrona do Python.**

---

## O que é "Backlog"?

No contexto de desenvolvimento de software, e especialmente em metodologias ágeis como Scrum ou Kanban, um "backlog" é uma **lista ordenada de itens (funcionalidades, requisitos, melhorias, bugs) que precisam ser desenvolvidos ou resolvidos em um produto.**

### Tipos Comuns de Backlog:

1. **Product Backlog (Backlog do Produto):**
    
    - É a lista mestra de tudo o que é conhecido que precisa ser feito para o produto.
        
    - É mantido e priorizado pelo **Product Owner** (Dono do Produto).
        
    - Os itens (chamados de "User Stories", "Épicos" ou "Bugs") são descrições de funcionalidades ou problemas, geralmente escritos de uma perspectiva de usuário.
        
    - Os itens no topo do backlog são os mais importantes, detalhados e prontos para serem trabalhados; os itens no final são menos detalhados e de menor prioridade.
        
2. **Sprint Backlog (Backlog da Sprint):**
    
    - Em Scrum, é um subconjunto do Product Backlog, contendo os itens que a equipe de desenvolvimento se compromete a entregar em uma "Sprint" (um período de tempo fixo, geralmente de 1 a 4 semanas).
        
    - É mantido e gerenciado pela **Equipe de Desenvolvimento**.
        

### Como o "Backlog" pode se relacionar com sua arquitetura (Uvicorn -> Backlog)?

A seta de "Uvicorn" para "Backlog" na sua imagem é um uso **não-convencional** do termo "Backlog" no contexto de arquitetura de sistema. Normalmente, um backlog é um conceito de gerenciamento de projeto, não um componente de sistema ativo que interage diretamente com um servidor web.

**Possíveis interpretações para "Backlog" na sua imagem:**

1. **Fila de Mensagens / Fila de Tarefas (Queue/Job Queue):**
    
    - Esta é a interpretação mais provável se "Backlog" for um componente de sistema.
        
    - Significa que o Uvicorn (ou a APP após receber a requisição) está enviando certas tarefas para uma **fila de processamento assíncrono**.
        
    - **Cenário:** O cliente faz uma requisição (ex: "enviar e-mail para 1000 usuários", "processar um relatório grande"). Essas tarefas demoram muito tempo e não devem bloquear a requisição HTTP. Então, a APP recebe a requisição, envia uma mensagem para uma fila (o "Backlog" neste caso), e imediatamente responde ao cliente (ex: "Sua requisição foi recebida e será processada").
        
    - **Tecnologias para isso:** RabbitMQ, Kafka, Redis Queue (RQ), Celery (com um broker como Redis ou RabbitMQ).
        
    - Nesse caso, o "Backlog" seria uma **fila de mensagens ou de tarefas a serem processadas por um worker separado** (que não é o Uvicorn nem a APP principal).
        
2. **Log de Requisições / Auditoria:**
    
    - Menos provável, mas possível: O Uvicorn (ou um componente antes/depois dele) estaria logando todas as requisições para algum tipo de sistema de backlog ou auditoria para análise posterior.
        
3. **Metáfora para Gerenciamento:**
    
    - Pode ser uma representação simplificada de que as requisições (ou informações sobre elas) de alguma forma alimentam o backlog de trabalho da equipe de desenvolvimento. Isso seria uma simplificação de um processo de feedback de usuário/sistema para o gerenciamento de projeto.
        

**Dado o contexto de um diagrama de fluxo de sistema, a interpretação como uma `fila de mensagens` para processamento assíncrono é a que faz mais sentido tecnicamente.**

---

Espero que esta explicação detalhada de Uvicorn e Backlog ajude a esclarecer o papel deles na sua arquitetura!