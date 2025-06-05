
---

Cada administração de rede pode querer controlar o roteamento na sua
própria rede. Ai que surgem os  “sistemas autônomos ” (AS).

- **Roteamento Intra-AS:** Dentro de cada AS, os roteadores executam o mesmo protocolo de roteamento. Esses protocolos são responsáveis por estabelecer entradas de roteamento para destinos localizados _dentro_ do mesmo AS.
- **Roteamento Inter-AS:** Refere-se aos protocolos de roteamento usados para trocar informações de roteamento _entre_ diferentes AS. 
- **Roteadores Gateway:** São roteadores que possuem links diretos para roteadores em outros AS. 

![[Pasted image 20250605152214.png]]



Vamos suSuponha que um roteador no AS1 receba um datagrama cujo destino seja
fora do AS1.
 O roteador deveria encaminhar o pacote para os roteadores gateway,
mas qual deles?
AS1 precisa:
1.Aprender quais destinos são alcancáveis através de AS2 e através de AS3.
2.Propagar suas informações de alcance para todos os roteadores em AS1.
Tarefa para o roteamento inter-AS routing!