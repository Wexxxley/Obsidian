
___

**Q1**
**"Um sistema distribuído é aquele no qual os componentes de hardware ou software, localizados em computadores interligados em rede, comunicam-se e coordenam suas ações apenas enviando mensagens entre si."**

**Com base na definição apresentada e nos conceitos básicos de sistemas distribuídos, assinale a opção correta.**

a. A falha de um componente em um sistema distribuído peer-to-peer causa a interrupção de todos os demais componentes até o seu retorno.  

==b. A adição de novos dispositivos em um sistema distribuído para atender a uma demanda temporária ou crescente está ligada à característica de escalabilidade do sistema.==

c. A possibilidade de vários clientes acessarem de forma concorrente um mesmo recurso compartilhado em um servidor é resultado do alto nível de transparência do sistema.

d. O compartilhamento dos recursos distribuídos entre computadores interligados por uma rede é possível desde que os dispositivos sejam homogêneos em termos de hardware e software. 

e. A existência de um relógio físico local sincronizado com um relógio global é o que permite aos usuários de um sistema distribuído trocarem mensagens de forma coordenada.

---

**Q2 A respeito de sistemas distribuídos, julgue o item a seguir.** 

**A política de segurança da ePING exige que informações classificadas e sensíveis transitem em redes inseguras com a devida criptografia, o que impede o acesso por pessoa não autorizada.**

==CORRETA. A exigência de que dados sensíveis transitem em redes públicas apenas de forma criptografada é uma diretriz básica e obrigatória em qualquer política de segurança séria, incluindo a ePING.==

---
**Q3 Um sistema de processamento distribuído ou paralelo é definido como um sistema que interliga vários nós de processamento de maneira que um processo de grande consumo seja executado no nó "mais disponível", ou mesmo subdividido por vários nós. Sobre sistemas distribuídos, analise as afirmativas a seguir:**

**I. Segurança: A criptografia pode ser usada para proporcionar proteção adequada para os recursos compartilhados e para manter informações sigilosas em segredo, quando transmitidas em mensagens de uma rede. Com isso, os ataques de negação de serviço deixaram de ser um problema.** 

**II. Escalabilidade: um sistema distribuído é considerado escalável se o custo de adição de um usuário for um valor variável, em termos dos recursos que devem ser adicionados. Os algoritmos usados para acessar os dados compartilhados devem evitar gargalos de desempenho, e os dados devem ser estruturados aleatoriamente para se obter os melhores tempos de acesso.** 

**III. Concorrência: a presença de múltiplos usuários em um sistema destruído é uma fonte de pedidos concorrentes para seus recursos. Em ambiente concorrente, cada recurso deve ser projetado para manter a consistência nos estados de seus dados.**

**É correto o que se afirma**

==APENAS A 3==

---
**Q4 Em Sistemas Distribuídos, o conceito de transparência pode ser aplicado em vários aspectos. A Transparência de Replicação pode ser definida como:**

**Escolha uma opção:**

a. a transparência em que os usuários não podem dizer qual é a localização física de um recurso no sistema.

b. a transparência de que um recurso está sendo compartilhado por vários usuários concorrentes.

c. a ocultação das diferenças em representação de dados e o modo como os recursos podem ser acessados por usuários.

==d. a ocultação do fato de que existem duas ou mais cópias de um recurso.==

e. realocação de recursos enquanto estão sendo acessados sem que o usuário ou a aplicação percebam qualquer coisa.

---
**Q5 Um sistema distribuído é um conjunto de sistemas autônomos, interconectados por uma rede de comunicação, que se diferencia dos demais sistemas fracamente acoplados pela existência de um relacionamento mais forte entre os seus componentes.**

**Tais componentes**

a. podem estar localizados em uma rede local ou em uma rede distribuída, mas os tipos de sistemas operacionais que compõem o sistema distribuído devem ser necessariamente homogêneos.

==b. podem estar localizados em uma rede local ou em uma rede distribuída e os tipos de sistemas operacionais que compõem o sistema distribuído não precisam ser necessariamente homogêneos.== 

c. devem estar localizados em uma rede local e os tipos de sistemas operacionais que compõem o sistema distribuído devem ser necessariamente homogêneos.

d. devem estar localizados em uma rede local e os tipos de sistemas operacionais que compõem o sistema distribuído não precisam ser necessariamente homogêneos.

e. devem estar localizados em uma rede distribuída e os tipos de sistemas operacionais que compõem o sistema distribuído devem ser necessariamente homogêneos.

---
**Q6 Acerca do conceito de sistemas distribuídos, analise as proposições abaixo.**

1) **Um sistema distribuído é uma coleção de computadores autônomos conectados por uma rede e equipados com um sistema de software distribuído.**

2) **Um sistema distribuído é uma coleção de computadores independentes, que aparenta ao usuário ser um computador único.**

3) **Em um sistema distribuído a falha de um computador do qual nunca se ouviu falar faz com que seu computador ou software pare completamente de funcionar.**

4) **multiprocessadores são sistemas fortemente acoplados, enquanto que multicomputadores são sistemas fracamente acoplados.**

Estão corretas:
==1, 2 e 4==

- **Sistemas fortemente acoplados** (como multiprocessadores) são compostos por vários processadores que geralmente compartilham a mesma memória e um relógio comum.
- **Sistemas fracamente acoplados** (como multicomputadores ou um sistema distribuído) são formados por um conjunto de computadores independentes, cada um com sua própria memória, interligados por uma rede.

---
**Q7 Segundo Andrew Tanembaum (2007) “Sistema Distribuído é uma coleção de computadores independentes que se apresenta ao usuário como um sistema único e consistente”. Assinale a alternativa correta a respeito de um sistema de informação distribuído.**

**Escolha uma opção:**

a. A distribuição de tarefas se dá a partir de requisições do usuário, que indica o endereço do servidor onde deseja executar tal tarefa.

b. Todos os computadores de uma rede executam tarefas de cliente e servidor, quando se deseja integrá-los em uma arquitetura de sistemas distribuídos.

c. A **transparência de acesso** é uma característica dos sistemas distribuídos que permite que recursos sejam acessados sem que sua localização seja determinada.

d. Em uma rede de computadores há servidores dedicados a atender pedidos dos clientes e estes, por sua vez, têm função exclusiva de requisitantes.

==e. Em um sistema de objetos distribuídos é possível invocar métodos de um objeto, ainda que este não esteja presente no computador do usuário.==

---
**Q8 A respeito de sistemas distribuídos, julgue o item a seguir.** 

 **Middleware é um sistema que conecta outros recursos, abstraindo protocolos de comunicação e camadas de infraestrutura.**

==Certo==

---
**Q9 Em sistemas distribuídos o middleware é uma camada adicional de software, situada entre o nível de aplicação e o nível que consiste no sistema operacional, que se estende por várias máquinas fornecendo uma abstração para a programação de aplicações em rede.**

**Assinale a alternativa que representa exemplos de middelware:**

**Escolha uma opção:**

==a. JAVA RMI e CORBA== 
b. JAVA e MICROSOFT DCOM
c. MICROSOFT RMI e JAVA DCOM
d. CORBA e JAVA
e. MICROSOFT RMI e CORBA

---
**Q10 Com relação a redes peer-to-peer (P2P), julgue os itens subsecutivos. O principal objetivo de se usar DHT (distributed hash table) em redes P2P descentralizadas e estruturadas é permitir que cada peer tenha informação total sobre seus vizinhos.**

==ERRADO==

O principal objetivo de se usar uma DHT não é permitir que cada peer tenha informação total sobre seus vizinhos. Pelo contrário, o objetivo é criar um sistema de busca eficiente e escalável, onde cada peer precisa manter informações sobre apenas um **pequeno e seleto número de outros peers**.

---
**Q11**
![](attachments/Pasted%20image%2020250930143401.png)

==cliente-servidor − servidor − cliente − cliente-servidor − cliente − servidor − sites==