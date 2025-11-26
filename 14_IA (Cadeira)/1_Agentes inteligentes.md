
#Concluded 

---
### **1. Agentes**

Um **Agente** é um sistema de software que pode perceber seu **Ambiente** através de **Sensores** e agir sobre esse ambiente através de **Atuadores**.

![400](../attachments/Pasted%20image%2020251108180452.png)

Exemplo: O Robô Aspirador de Pó Este exemplo é usado para ilustrar os conceitos:

- **Agente:** O robô aspirador.    
- **Sensores:** Sensores de penhasco (Cliff Sensor), sensor de sujeira, etc..
- **Atuadores:** Extratores de detritos (Debris Extractors), escova lateral (Side Brush), rodas.

- **Ambiente:** Um mundo com duas localizações, A e B.
- **Percepções:** Localização, Estado (ex: `[A, Limpo]`, `[A, Sujo]`).
- **Ações:** Mover para Direita, Mover para Esquerda, Aspirar.
![400](../attachments/Pasted%20image%2020251108181036.png)

---
### **2. Agentes Racionais**

Um Agente Racional é <mark style="background: #ADCCFFA6;">aquele que age para maximizar sua medida de desempenho.</mark>

- **Racionalidade vs. Perfeição:** Ser racional não significa ser perfeito. 
    - "Um agente jogador de pôquer racional nunca perde?". O agente pode perder se seu oponente tiver cartas melhores. 
	- <mark style="background: #ADCCFFA6;">Racionalidade é tomar a melhor decisão com base nas percepções disponíveis.</mark>

---
### 3. O Framework PEAS

Para projetar um agente racional, os slides introduzem o framework **PEAS**:

- **P**erformance (Medida de Desempenho)
- **E**nvironment (Ambiente)
- **A**ctuators (Atuadores)
- **S**ensors (Sensores)

---
### 4. A Natureza dos Ambientes

**Completamente Observável:** O agente tem acesso ao estado completo do ambiente em todos os momentos.  (Ex: Um jogo de xadrez, onde o agente vê todas as peças no tabuleiro).
    
**Parcialmente Observável:** O agente _não_ tem acesso ao estado completo. Isso pode ocorrer porque os sensores não captam tudo (ex: um robô vendo apenas o que está à sua frente) ou porque parte da informação está oculta (ex: as cartas do oponente em um jogo de pôquer).

---
**Agente Único:** O agente opera sozinho no ambiente. Não há outros agentes cujas ações precisem ser consideradas.
    
**Multiagente:** Existem outros agentes no ambiente que também percebem e atuam. Esses outros agentes podem ser **competitivos** (como em um jogo, onde tentam vencer o agente) ou **cooperativos** (como em um time de robôs de futebol).

---
**Determinístico:** O próximo estado do ambiente é totalmente previsível com base no estado atual e na ação do agente. Se o agente executa a ação "A" no estado "X", o resultado será _sempre_ o estado "Y".
    
**Estocástico:** O próximo estado do ambiente não é totalmente determinado; há um elemento de aleatoriedade ou probabilidade. (Ex: um carro autônomo não pode prever com certeza se o freio de outro carro falhará).

---
**Episódico:** A experiência do agente é dividida em "episódios" independentes. Em cada episódio, o agente percebe o ambiente e realiza uma única ação. A ação tomada em um episódio não afeta os episódios futuros. (Ex: Um sistema que classifica imagens uma por uma).
    
**Sequencial:** As decisões atuais afetam todas as decisões futuras. O agente precisa planejar a longo prazo, pois suas ações têm consequências duradouras. (Ex: Em um jogo de xadrez, uma má jogada agora pode levar à derrota muitas jogadas depois).

---
**Estático:** O ambiente não muda enquanto o agente está "pensando" ou decidindo qual ação tomar. O agente pode levar o tempo que precisar para deliberar.
    
**Dinâmico:** O ambiente pode mudar enquanto o agente está pensando. Isso o força a tomar decisões rapidamente. (Ex: Dirigir um carro em tráfego intenso).

---
**Discreto:** O estado do ambiente, o tempo e as ações do agente são finitos ou contáveis. (Ex: Jogo de xadrez, com um número finito de casas e peças).
    
**Contínuo:** O estado, o tempo ou as ações assumem valores em um intervalo contínuo (números reais). (Ex: Dirigir um carro, onde a velocidade, a posição e o ângulo do volante são valores contínuos).

---
**Conhecido:** O agente conhece as "regras" do ambiente. Ele sabe quais são os resultados de suas ações (ou as probabilidades de resultados, se for estocástico).
    
**Desconhecido:** O agente não sabe como o ambiente funciona e deve primeiro explorá-lo para aprender suas regras e como suas ações afetam o estado.