
---

### **1. Roteamento hierárquico**
Cada administração de rede pode querer controlar o roteamento na sua
própria rede. Ai que surgem os  “sistemas autônomos ” (AS).

- **Roteamento Intra-AS:** Dentro de cada AS, os roteadores executam o mesmo protocolo de roteamento. Esses protocolos são responsáveis por estabelecer entradas de roteamento para destinos localizados _dentro_ do mesmo AS.
- **Roteamento Inter-AS:** Refere-se aos protocolos de roteamento usados para trocar informações de roteamento _entre_ diferentes AS. 
- **Roteadores Gateway:** São roteadores que possuem links diretos para roteadores em outros AS. 

![[Pasted image 20250605152214.png]]

Quando um roteador no AS1 recebe um datagrama cujo destino está fora do AS1, ele não possui, por si só, essa informação. É aqui que entram os protocolos de roteamento inter-AS e intra-AS.

**1. Aprender quais destinos são alcançáveis através de AS2 e através de AS3.**
- **Tarefa para o roteamento inter-AS!** Os roteadores de _gateway_ do AS1 estabelecem sessões BGP (Border Gateway Protocol) com os roteadores de _gateway_ dos ASs vizinhos. Através dessas sessões, o AS1 aprende sobre as sub-redes que são anunciadas por AS2 e AS3. 

**2. Propagar suas informações de alcance para todos os roteadores em AS1.**
- Uma vez que os roteadores de _gateway_ do AS1 aprendem sobre os destinos externos, essa informação precisa ser distribuída para os demais roteadores dentro do AS1. **Isso é feito pelo protocolo intra-AS.** 

**Cenário: AS1 aprende que a sub-rede 'x' é alcançável através de AS3 e através de AS2.**
- **Roteamento de “batata-quente”
    - A ideia da "batata-quente" é que o AS local quer se livrar do pacote o mais rápido possível, encaminhando-o para o ponto de saída mais próximo em termos de métrica interna 

---
### **2. Protocolos de roteamento intra AS**

#### **2.1 RIP**
- Ultiliza o algoritmo de vetor de distancia
- A métrica que o RIP usa para determinar a "melhor" rota para é a **contagem de saltos**. A rota com o menor número de saltos é considerada a melhor. (MÁXIMO 15 SALTOS).
- Uma rota é mantida somente para cada destino.
- A RIP faz a troca Periódica de Tabelas de roteamento, or padrão, essa troca ocorre a cada 30 s.
- Com 180s sem retornos, o roteador considera o seu vizinho morto, descarta as rotas que passam por ele e avisa seus vizinhos.
![[Pasted image 20250605154808.png]]
- RIP V1: Sem criptografia,
- RIP V2: Tem criptografia, 














