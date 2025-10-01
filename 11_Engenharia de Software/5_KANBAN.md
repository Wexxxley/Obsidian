

---
Kanban é um método que visa ajudar as equipes a encontrar um ritmo de trabalho sustentável, eliminando desperdícios e focando em melhorias contínuas. Sua origem remonta ao sistema de produção _just-in-time_ da Toyota, na década de 1950, e foi adaptado para o desenvolvimento de software pela primeira vez na Microsoft, em 2004.
### **1. Diferenças entre Kanban e Scrum**
Kanban é mais simples que o Scrum e se diferencia nos seguintes pontos:

- **Não utiliza eventos**: Não há _sprints_, reuniões diárias, de revisão ou retrospectivas, embora a equipe possa adotá-los se julgar necessário.
- **Não define papéis rígidos**: Kanban não define papéis como PO ou _Scrum Master_.
- **Foco no Quadro de Tarefas**: O único artefato central é o **Quadro Kanban**, que inclui o _Backlog do Produto_ e visualiza todo o fluxo de trabalho.

### **2. O Quadro Kanban e o Fluxo de Trabalho**

O Quadro Kanban é o coração do método e é dividido em colunas que representam as etapas do processo de desenvolvimento.

- **Backlog do Produto**: A primeira coluna contém as histórias, que, assim como no Scrum, são escritas pelos usuários.
- **Etapas do Processo**: As colunas seguintes representam os passos necessários para transformar uma história em uma funcionalidade pronta. Por exemplo: **Especificação**, **Implementação** e **Revisão de Código**.
- **Subcolunas "Em execução" e "Concluídas"**: Cada etapa é dividida em duas subcolunas. As tarefas "concluídas" em uma etapa aguardam para serem "puxadas" para a etapa seguinte. Por isso, Kanban é chamado de **sistema _pull_**: os membros da equipe puxam o trabalho conforme sua capacidade, em vez de o trabalho ser empurrado para eles.

As equipes Kanban são **auto-organizáveis** e **multidisciplinares** (_cross-functional_), tendo autonomia para decidir qual tarefa puxar para o próximo passo e possuindo todas as habilidades necessárias para completar o trabalho.

![](attachments/Pasted%20image%2020251001180709.png)
#### Limites WIP (Work in Progress)

Para garantir um ritmo de trabalho sustentável e evitar sobrecarga, Kanban utiliza os **Limites WIP**. Eles definem o **número máximo de tarefas** que podem estar em cada etapa do quadro, somando as tarefas "em execução" e "concluídas" (com exceção da última etapa, onde o limite se aplica apenas às tarefas em andamento).

**O objetivo principal dos limites WIP é evitar que a equipe fique sobrecarregada**, pois o excesso de tarefas simultâneas tende a diminuir a qualidade do trabalho. Esses limites funcionam como uma "trava" que impede a equipe de aceitar mais trabalho do que sua capacidade, servindo como um mecanismo de defesa contra pressões externas, como as de gerentes. O cálculo desses limites pode ser feito aplicando-se a **Lei de Little**, uma fórmula da Teoria de Filas que relaciona o WIP com o tempo médio de execução de uma tarefa (_lead time_) e a vazão do processo (_throughput_).

---

Com isso, finalizamos a explicação sobre Kanban e as principais metodologias ágeis do Capítulo 2. Diga "next" para prosseguirmos com a discussão sobre quando os métodos ágeis não são recomendados.