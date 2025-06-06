
#Concluded 

---

 Um pacote de camada de rede é denominado um **datagrama**. Os principais campos do datagrama ipv4 são os seguintes: 
 - **Número da versão** 
 - **Comprimento cabeçalho:** Um datagrama IPv4 pode conter um número variável de opções, esses bits são necessários para determinar onde, no datagrama, os dados começam de fato. Normalmente datagramas não usam opções; o datagrama típico tem um cabeçalho de **2 bytes.**
 - **Tipo de serviço:** Usados para poder diferenciar os diferentes tipos serviço (que requerem baixo atraso, alta vazão ou confiabilidade) 
 - **Comprimento do datagrama.** É o comprimento total do datagrama (cabeçalho mais dados).
 - **Identificador, flags, deslocamento de fragmentação:** ampos têm a ver com a fragmentação.
 - **Tempo de vida:** O campo de tempo de vida é incluído para garantir que datagramas não fiquem circulando para sempre.  Esse campo é decrementado e, uma unidade cada vez que o datagrama é processado por um roteador, ou seja, virou um ==número máximo de saltos.==
![[Pasted image 20250523103049.png]]
- **Protocolo:** Usado  quando o datagrama chega a seu destino. O campo indica o protocolo de camada de transporte.
- **Soma de verificação do cabeçalho:** A soma de verificação do cabeçalho auxilia um roteador na detecção de erros de bits em um datagrama IP recebido. 
- **Endereços IP de origem e de destino:** Auto explicativo.
- **Opções**: A intenção é que as opções de cabeçalho sejam usadas raramente.
- **Dados:** Em muitas circunstâncias, o campo de dados do datagrama IP contém o segmento da camada de transporte (TCP ou UDP) a ser entregue ao destino. Contudo, o campo de dados pode carregar outros tipos de dados, como mensagens ICMP.