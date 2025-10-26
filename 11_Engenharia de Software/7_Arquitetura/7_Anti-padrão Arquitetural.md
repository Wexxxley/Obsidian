
#Concluded 

---

Enquanto os padrões arquiteturais descrevem boas práticas e soluções comprovadas para organizar sistemas, um anti-padrão descreve uma "solução" comum, mas ineficaz ou problemática, para um problema recorrente. Reconhecer anti-padrões ajuda a evitá-los.

**Big Ball of Mud:**
- <mark style="background: #ADCCFFA6;">Termo é usado para descrever sistemas que não possuem uma arquitetura reconhecível.</mark>
- São sistemas onde a estrutura se deteriorou ao longo do tempo, resultando em um emaranhado de dependências entre seus módulos ou componentes.
    
- **Características Típicas:**
    - Falta de estrutura clara (ausência de camadas, módulos bem definidos, etc.).
    - Alto acoplamento entre diferentes partes do sistema.
    - Baixa coesão dentro dos módulos (módulos fazem "um pouco de tudo").
    - Dificuldade em entender, modificar, testar ou evoluir o sistema. Qualquer pequena mudança pode ter efeitos colaterais inesperados em partes aparentemente não relacionadas.

Embora seja um anti-padrão, é surpreendentemente comum na indústria, especialmente em sistemas legados que evoluíram por muito tempo sem o devido cuidado arquitetural. Evitá-lo requer disciplina, atenção contínua à arquitetura, refatoração e boas práticas de design ao longo de todo o ciclo de vida do software.
