Status: #Concluded 

___

Álgumas aplicações podem funcionar melhor de acordo com o protocolo da camada de transporte utilizado. [1_Protocolos da camada de transporte da internet](../3_Camada%20de%20Transporte/1_Protocolos%20da%20camada%20de%20transporte%20da%20internet.md)

# 1 Requisitos das aplicações

- Algumas aplicações (como vídeos e áudios em tempo real) podem tolerar alguma **perda de dados**. Outras(como a transferência de arquivos) exigem transferência 100% confiável.
- Algumas aplicações (como telefonia, jogos interativos) são **sensíveis ao atraso** (latencia baixa) e exigem baixos atrasos para serem “efetivos”.
- Algumas aplicações (como streaming, jogos online) exigem uma **taxa de transferência mínima**. Outras (“aplicações elásticas”) se adequam a quantidade de banda passante sem grandes prejuízos(como download, navegar na web).

 

![](https://lh7-rt.googleusercontent.com/docsz/AD_4nXdYAH_NdfY54_Ei075veZkSQFSGkpply2TuQt3lh8EbC3dBYPdWrvzdRUdKTKbnbZNnwuYagXdpogtBlLDpAHxnw09Ltl6TjjnAIFmn_edbnR5hiEIWbZPLWBFpV7qo9TTtyw_L3w?key=HrOhHC0_-ked6RNCpQ0o3PZn)

O UDP domina aplicações em tempo real porque:

- Entrega dados mais rápido, mesmo com perdas ocasionais.
- Evita atrasos causados pelo TCP (handshake, retransmissões, controle de fluxo).
- É a escolha ideal quando "tempo real" > "perfeição".

Enquanto o TCP é ótimo para **downloads, emails e páginas web**.
