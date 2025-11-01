
#Concluded 

---
Kanban é um método que <mark style="background: #ADCCFFA6;">visa ajudar as equipes a encontrar um ritmo de trabalho sustentável</mark>, eliminando desperdícios e focando em melhorias contínuas. Sua origem remonta ao sistema de produção _just-in-time_ da Toyota, na década de 1950, e foi adaptado para o desenvolvimento de software pela primeira vez na Microsoft, em 2004.
### **1. Diferenças entre Kanban e Scrum**
Kanban é mais simples que o Scrum e se diferencia nos seguintes pontos:

- **Não utiliza eventos**: Não há _sprints_, reuniões diárias, de revisão ou retrospectivas, embora a equipe possa adotá-los se julgar necessário.
- **Não define papéis rígidos**: Kanban não define papéis como PO ou _Scrum Master_.
- **Foco no Quadro de Tarefas**: O único artefato central é o **Quadro Kanban**, que inclui o _Backlog do Produto_ e visualiza todo o fluxo de trabalho.

---
### **2. O Quadro Kanban e o Fluxo de Trabalho**

O Quadro Kanban é o coração do método e é  totalmente customizável, mas geralmente segue essa estrutura:
![](attachments/Pasted%20image%2020251001181025.png)

- **Backlog do Produto**: A primeira coluna contém as histórias de usuários.
- **Etapas do Processo**: As colunas seguintes representam os passos necessários para transformar uma história em uma funcionalidade pronta. Por exemplo: **Especificação**, **Implementação** e **Revisão de Código**.
- **Subcolunas**: Cada etapa é dividida em duas subcolunas. As tarefas "concluídas" em uma etapa aguardam para serem "puxadas" para a etapa seguinte. Os membros da equipe puxam o trabalho conforme sua capacidade, em vez de o trabalho ser empurrado para eles.

---
### **3. Limites WIP (Work in Progress)**

Para garantir um ritmo de trabalho sustentável, Kanban utiliza os **Limites WIP**. Eles definem o **número máximo de tarefas** que podem estar em cada etapa do quadro, somando as tarefas "em execução" e "concluídas" (com exceção da última etapa, onde o limite se aplica apenas às tarefas em andamento).

**O objetivo principal dos limites WIP é evitar que a equipe fique sobrecarregada**, pois o excesso de tarefas simultâneas tende a diminuir a qualidade do trabalho.  

---
### 4. Prinípios e práticas 

**Princípios:**

- Visualização do Trabalho: Todo o fluxo de trabalho deve ser visível para o time, através do Quadro Kanban.
    
- Limitação do Trabalho em Progresso (WIP): O princípio fundamental é evitar a sobrecarga do time. Em vez de "empurrar" trabalho, o time "puxa" novas tarefas apenas quando há capacidade.
    
- Gestão do Fluxo: O foco é otimizar o fluxo de trabalho, identificando e eliminando gargalos para que as tarefas se movam suavemente do início ao fim.
    
- Melhoria Contínua: A equipe deve analisar seu fluxo (visualizado no quadro) para fazer melhorias constantes.
    
**Práticas:**

- Quadro Kanban: O quadro é dividido em colunas que representam os passos do fluxo de trabalho da equipe (ex: Backlog, Especificação, Implementação, Revisão de Código, Concluído).
    
- Limites WIP (Work in Progress): Cada coluna do fluxo de trabalho (exceto o backlog e a coluna final "Done") recebe um limite numérico explícito de quantas tarefas podem estar nela ao mesmo tempo. O objetivo é prevenir sobrecarga e garantir um ritmo sustentável.
    
- Sistema Pull: Novas tarefas não são "empurradas" para a próxima etapa. Uma etapa só "puxa" uma nova tarefa da coluna anterior quando ela tem capacidade.
    