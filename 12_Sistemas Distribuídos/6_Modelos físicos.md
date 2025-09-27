
#Concluded 

---
#### **1.1 Modelo físico básico** 
Um modelo físico básico é um ==conjunto extensível de nós de computador interconectados por uma rede de computadores para troca de mensagens.==

**Sistemas distribuídos primitivos**: Surgiram no final dos anos 1970 em resposta ao surgimento da tecnologia de redes locais. Esses sistemas consistiam em algo entre 10 e 100 nós interconectados por uma ==rede local, suportando uma pequena variedade de serviços==, como impressoras, servidores de arquivos compartilhados,  e transferências de e-mail. Não havia muita preocupação com o fato de serem abertos. 
#### **1.2 Sistemas distribuídos adaptados para a Internet:**
Aproveitando essa base, S.D de maior escala começaram a surgir nos anos 1990, em resposta crescimento da Internet. Nesses sistemas, a infraestrutura consiste em um modelo que é um ==conjunto extensí-vel de nós interconectados por uma rede de redes. Esses sistemas exploravam a infraestrutura oferecida pela Internet para desenvolver sistemas distribuídos realmente globais==, envolvendo potencialmente grandes números de nós.  Como resultado, o nível de **heterogeneidade** nesses sistemas era significativo em termos de redes, arquiteturas de computador, sistemas operacionais, linguagens e também equipes de desenvolvimento envolvidas. Isso levou a uma ênfase cada vez maior em padrões abertos e tecnologias de middleware associadas.
#### **1.3 Sistemas distribuídos contemporâneos:**
Nos sistemas anteriores, os nós normalmente eram relativamente **estáticos**, **separados** e **autônomos**. As principais tendências que resultaram em desenvolvimentos significativos nos modelo físicos são:
1. A **computação móvel** levou a modelos físicos em que nós como smartphones podem mudar de um lugar, levando à necessidade de mais recursos, como a descoberta de serviço e o suporte para operação conjunta espontânea.
2. A **computação ubíqua** levou à mudança de nós distintos para arquiteturas em que os computadores são incorporados em objetos comuns e no ambiente circundante.
3. A **computação em nuvem** e, em particular, das arquiteturas de agregados (clusters), levou a uma mudança de nós autônomos para conjuntos de nós que, juntos, fornecem determinado serviço.
#### **1.4 Sistemas distribuídos de sistemas**
Um sistema de sistemas pode ser definido como um sistema complexo, consistindo em uma série de subsistemas, os quais são, eles próprios, sistemas que se reúnem para executar uma ou mais tarefas em particular.

Como exemplo de sistema de sistemas, considere um sistema de gerenciamento ambiental para previsão de enchentes. Nesse cenário, existirão redes de sensores implantadas para monitorar o estado de vários parâmetros ambientais; Isso pode, então, ser acoplado a sistemas responsáveis por prever a probabilidade de enchentes, fazendo simulações em clusters. Outros sistemas podem ser estabelecidos para manter e analisar dados históricos .