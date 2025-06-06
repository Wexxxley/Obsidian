
---

 Um pacote de camada de rede é denominado um **datagrama**. Os principais campos do datagrama ipv4 são os seguintes: 
 - **Número da versão:** Quatro bits especificam a versão do protocolo IP do datagrama. 
 - **Comprimento do cabeçalho:** Como um datagrama IPv4 pode conter um número variável de opções, esses quatro bits são necessários para determinar onde, no datagrama IP, os dados começam de fato. A maior parte dos datagramas não contém opções; o datagrama IP típico tem um cabeçalho de **20 bytes.** 
 - **Tipo de serviço:** Usados para poder diferenciar os diferentes tipos de datagramas IP (que requerem baixo atraso, alta vazão ou confiabilidade) que devem ser distinguidos uns dos outros.
 - **Comprimento do datagrama.** É o comprimento total do datagrama IP (cabeçalho mais dados).
 - **Identificador, flags, deslocamento de fragmentação:** Esses três campos têm a ver com a fragmentação.
 - **Tempo de vida:** O campo de tempo de vida é incluído para garantir que datagramas não fiquem circulando para sempre.  Esse campo é decrementado e, uma unidade cada vez que o datagrama é processado por um roteador, ou seja, virou um ==número máximo de saltos.==
![[Pasted image 20250523103049.png]]
- **Protocolo:** Usado  quando o datagrama chega a seu destino. O campo indica o protocolo de camada de transporte.
- **Soma de verificação do cabeçalho:** A soma de verificação do cabeçalho auxilia um roteador na detecção de erros de bits em um datagrama IP recebido. 
- **Endereços IP de origem e de destino:** Auto explicativo.
- **Opções**: A intenção é que as opções de cabeçalho sejam usadas raramente.
- **Dados:** Em muitas circunstâncias, o campo de dados do datagrama IP contém o segmento da camada de transporte (TCP ou UDP) a ser entregue ao destino. Contudo, o campo de dados pode carregar outros tipos de dados, como mensagens ICMP.