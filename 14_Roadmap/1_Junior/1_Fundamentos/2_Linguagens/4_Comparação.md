
#Concluded 

---
### 1. Onde Cada Tipo de Linguagem é Mais Usada?

#### 1.1 Compiladas (C, C++, Go)

Onde o Desempenho Bruto e o Acesso ao Hardware são Reis. Essas linguagens são usadas quando a velocidade e o controle de memória são a prioridade máxima e inegociável.

- **C:** Sistemas Operacionais (o coração do Linux, Windows, macOS), Sistemas Embarcados (o software da sua geladeira, micro-ondas, carro), drivers de hardware. 
        
- **C++:** Motores de Jogos (Unreal Engine), software de simulação em tempo real (aviação, finanças), software gráfico (Adobe Photoshop) e sistemas embarcados grandes.
        
- **Go:** Infraestrutura de nuvem (Docker e Kubernetes são feitos em Go), serviços de backend que precisam lidar com milhares de conexões ao mesmo tempo.        

#### 1.2 Híbridas (Java, C#)

O Padrão para Grandes Aplicações Corporativas e de Larga Escala. Essas linguagens oferecem o melhor dos dois mundos: são portáteis (rodam em qualquer lugar) e, graças ao JIT, têm um desempenho excelente após o "aquecimento".

- **Java:** Grandes sistemas de backend corporativos (bancos, e-commerces, seguradoras), aplicações de Big Data (Hadoop, Spark) e desenvolvimento de aplicativos Android.
        
- **C#:**  Aplicações corporativas no ecossistema Microsoft (.NET), desenvolvimento de jogos (a linguagem principal da **Unity**) e aplicações web (ASP.NET).

#### 1.3 Interpretadas (Python, JavaScript, Ruby)

Essas linguagens dominam onde a rapidez para construir, prototipar e automatizar é mais importante que o último pingo de performance da CPU.

- **JavaScript (com Node.js):** A linguagem da web. O desenvolvimento Front-end (React, Angular, Vue). No backend (Node.js), é fantástica para aplicações I/O-bound  e microserviços.
        
- **Python:** Rei absoluto de Data Science, Machine Learning e Inteligência Artificial (Pandas, TensorFlow, PyTorch). Também muito usada em backend web (Django, Flask) e scripts de automação.
        
- **Ruby:** Backend web, especialmente com o framework Ruby on Rails.

---
### **2. Testes de Desempenho** 

> **Aviso Importante:** A maioria das aplicações web não são limitadas pela CPU. Elas são <mark style="background: #ADCCFFA6;">I/O-bound, o que significa que o gargalo é a lentidão da rede ou a espera por uma consulta ao banco de dados</mark>. É por isso que o Node.js (lento em CPU, rápido em I/O) e o Python (lento em CPU, rápido para desenvolver) são tão populares.

#### Tier 1: Performance Bruta (C, C++, Rust)

- **Resultado:** São os reis indiscutíveis da velocidade.    
#### Tier 2: Desempenho de Pico (Java, C#, Go)

- **Resultado:** Surpreendentemente próximos do Tier 1, especialmente após o "aquecimento" do JIT. O JIT otimiza o código _enquanto ele roda_, às vezes fazendo otimizações que um compilador estático (como o do C++) não poderia prever.

#### Tier 3: Foco na Produtividade (Python, Ruby)

- **Resultado:** São significativamente mais lentos em tarefas de CPU.
    
- **Por quê:** O interpretador padrão do Python (CPython) não usa JIT. Ele foca na compatibilidade e simplicidade, não na velocidade de execução.
    
- **O Dado:** A mesma tarefa que o **C levou 1.23 segundos**, o **Python (CPython) levou 126.53 segundos**. 