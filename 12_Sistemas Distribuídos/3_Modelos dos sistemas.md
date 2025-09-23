

---
Mostramos como as **propriedades** e os **problemas** de projeto de sistemas distribuídos **podem ser capturados e discutidos por meio do uso de modelos descritivos**. Cada tipo de modelo é destinado a fornecer uma descrição abstrata e simplificada de um aspecto relevante.

1. Os **modelos físicos** são a maneira mais explítica de descrever um sistema; eles capturam a composição de hardware de um sistema, em termos dos computadores e suas redes de interconexão.

2. Os **modelos de arquitetura** descrevem um sistema em termos das tarefas computacionais e de comunicação realizadas por seus elementos computacionais – os computadores individuais ou seus agregados (clusters) suportados pelas interconexões de rede apropriadas.

3. Os **modelos fundamentais** adotam uma perspectiva abstrata para examinar os aspectos individuais de um sistema distribuído.
	1. **modelos de interação**, que consideram a estrutura e a ordenação da comunicação entre os elementos do sistema; 
	2. **modelos de falha,** que consideram as maneiras pelas quais um sistema pode deixar de funcionar corretamente;
	3. **modelos de segurança**, que consideram como o sistema está protegido contra tentativas de interferência em seu funcionamento correto ou de roubo de seus dados.

---
### **Modelo físico**
Um modelo físico é uma representação dos elementos de hardware de um sistema distribuído, de maneira a abstrair os detalhes específicos do computador e das tecnologias de rede empregadas.

**Modelo físico básico**: no Capítulo 1, um sistema distribuído foi definido como aquele no 
qual os componentes de hardware ou software localizados em computadores interligados 
em rede se comunicam e coordenam suas ações apenas passando mensagens. Isso leva a 
um modelo físico mínimo como sendo um conjunto extensível de nós de computador interconectados por uma rede de computadores para a necessária passagem de mensagens.

**Sistemas distribuídos primitivos**: esses sistemas surgiram no final dos anos 1970 e início 
dos anos 1980 em resposta ao surgimento da tecnologia de redes locais. Esses sistemas consistiam em algo entre 10 e 100 nós interconectados por uma rede local, suportando uma pequena variedade de serviços, como impressoras, servidores de arquivos compartilhados,  e transferências de e-mail. Não havia muita preocupação com o fato de serem abertos. 

**Sistemas distribuídos adaptados para a Internet:** aproveitando essa base, S.D de maior escala começaram a surgir nos anos 1990, em resposta crescimento da Internet. Nesses sistemas, a infraestrutura física consiste em um modelo que é um conjunto extensí-vel de nós interconectados por uma rede de redes (a Internet). Esses sistemas exploravam a infraestrutura oferecida pela Internet para desenvolver sistemas distribuídos realmente globais, envolvendo potencialmente grandes números de nós.  Como resultado, o nível de **heterogeneidade** nesses sistemas era significativo em termos de redes, arquiteturas de computador, sistemas operacionais, linguagens empregadas e também equipes de desenvolvimento envolvidas. Isso levou a uma ênfase cada 
vez maior em padrões abertos e tecnologias de middleware associadas.

**Sistemas distribuídos contemporâneos:** nos sistemas anteriores, os nós normalmente eram 
computadores de mesa e, portanto, relativamente estáticos, separados e autônomos. As principais tendências identificadas na Seção 
1.3 resultaram em desenvolvimentos significativos nos modelo físicos:
• O surgimento da computação móvel levou a modelos físicos em que nós como note￾books ou smartphones podem mudar de um lugar para outro em um sistema distribuí-
do, levando à necessidade de mais recursos, como a descoberta de serviço e o suporte 
para operação conjunta espontânea.