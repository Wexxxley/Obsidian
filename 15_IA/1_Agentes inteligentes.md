

---

![](../attachments/Pasted%20image%2020251108180452.png)


### 2. O Estado Atual da IA (O que é possível hoje?)

Os slides apresentam uma série de desafios para avaliar o que a IA consegue fazer atualmente. Para cada desafio, é dada uma breve avaliação do estado da arte:

- **Jogar pingue-pongue:** Considerado de nível intermediário.
    
- **Dirigir no centro de Quixadá:** Avaliado como "Ainda muito imprevisível para um robô".
    
- **Comprar mantimentos no mercado:** Difícil, principalmente pela manipulação de objetos e pelo ambiente "cheio".
    
- **Executar uma operação cirúrgica complexa:** Atualmente, ainda é necessária a supervisão médica.
    
- Outros desafios mencionados incluem descobrir teoremas matemáticos, escrever histórias engraçadas, dar assessoria jurídica e traduzir idiomas em tempo real.
    

### 3. O Conceito Central: Agentes e Ambientes

A aula introduz formalmente o conceito de "Agentes Inteligentes".

- **Definição:** Um **Agente** é qualquer coisa que pode perceber seu **Ambiente** através de **Sensores** e agir sobre esse ambiente através de **Atuadores**.
    
- **Fluxo:** O agente recebe **Percepções** dos sensores e, com base nelas, decide quais **Ações** executar.
    

**Exemplo: O Robô Aspirador de Pó** Este exemplo é usado para ilustrar os conceitos:

- **Agente:** O robô aspirador.
    
- **Sensores:** Sensores de penhasco (Cliff Sensor), sensor de sujeira, etc..
    
- **Atuadores:** Extratores de detritos (Debris Extractors), escova lateral (Side Brush), rodas.
    
- **Ambiente Simplificado:** Um mundo com duas localizações, A e B.
    
- **Percepções:** [Localização, Estado] (ex: `[A, Limpo]`, `[A, Sujo]`).
    
- **Ações:** Mover para Direita, Mover para Esquerda, Aspirar.
    

### 4. Agentes Racionais

A aula foca em um tipo específico de agente: o Agente Racional.

- **O que faz um agente "bom"?** A qualidade de um agente é definida por sua **medida de desempenho**.
    
- **Definição:** Um **Agente Racional** é aquele que age para **maximizar sua medida de desempenho**.
    
- **Medida de Desempenho (Exemplo do Aspirador):** A medida de desempenho é crucial. Ela é:
    
    - A quantidade de sujeira aspirada em 8 horas?
        
    - Recompensar o agente por deixar o chão limpo?
        
    - Penalizar o agente pela energia desperdiçada?
        
- **Racionalidade vs. Perfeição:** Ser racional não significa ser onisciente ou perfeito. Os slides usam o exemplo de um jogador de pôquer.
    
    - **Pergunta:** "Um agente jogador de pôquer racional nunca perde?".
        
    - **Resposta:** Não. "O agente pode perder se seu oponente tiver cartas melhores". Racionalidade é tomar a melhor decisão _com base nas percepções disponíveis_, e não saber o resultado de tudo.
        

### 5. Projeto de Agentes: O Framework PEAS

Para projetar um agente racional, os slides introduzem o framework **PEAS**:

- **P**erformance (Medida de Desempenho)
    
- **E**nvironment (Ambiente)
    
- **A**ctuators (Atuadores)
    
- **S**ensors (Sensores)
    

Os slides propõem uma atividade onde os alunos devem definir o PEAS para diferentes agentes, como um "Uber" sem motorista, um sistema de diagnóstico médico, o "Duolingo", um robô separador de peças ou o buscador "Google".

### 6. A Natureza dos Ambientes

Finalmente, a aula detalha como classificar os ambientes, pois o design do agente depende profundamente do ambiente em que ele atua.

As principais propriedades de um ambiente são:

- **Completamente x Parcialmente Observável:** O agente consegue ver o estado completo do ambiente?
    
- **Agente único x Multiagente:** O agente opera sozinho ou compete/coopera com outros agentes?
    
- **Determinístico x Estocástico:** O próximo estado do ambiente é totalmente determinado pela ação do agente ou há incerteza?
    
- **Episódico x Sequencial:** A experiência do agente é dividida em "episódios" independentes, ou a ação atual afeta todas as decisões futuras?
    
- **Estático x Dinâmico:** O ambiente pode mudar enquanto o agente está "pensando"?
    
- **Discreto x Contínuo:** As percepções, ações e o tempo são divididos em valores finitos ou são contínuos?
    
- **Conhecido x Desconhecido:** O agente conhece as "regras" do ambiente?
    

Os slides propõem uma segunda atividade para classificar ambientes como Jogo de Xadrez, Jogo de Pôquer, Carro autônomo e Diagnóstico médico, justificando cada característica.