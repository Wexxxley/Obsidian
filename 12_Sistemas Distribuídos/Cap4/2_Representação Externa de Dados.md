
#Concluded 

---
O principal desafio é que **diferentes computadores podem usar diferentes representações** para tipos de dados simples, como inteiros ou números de ponto flutuante (problema de heterogeneidade). O processo de transformar dados estruturados em uma sequência de bytes para transmissão é chamado de **empacotamento** (_marshalling_).

### 1. Empacotamento (Marshalling)
O empacotamento envolve a **serialização** (transformação em uma sequência de bytes) dos valores primitivos e dos tipos de dados estruturados. O processo inverso, chamado **desempacotamento** (_unmarshalling_), reconstrói a representação de dados a partir dos valores primitivos recebidos.

**Problema**: Diferentes arquiteturas usam ordens de bytes distintas para representar valores (como inteiros de 32 bits). É necessário uma representação externa sobre a ordem de bytes a ser usada na transmissão de um valor de dados.

Estratégias de representação externa
1. **Representação Comum de Dados (CDR) do CORBA:** É uma representação externa dos tipos primitivos e estruturados que podem ser passados como argumentos e resultados na Invocação de Métodos Remotos (RMI) do CORBA. O CDR é independente da linguagem de programação.
2. **Serialização Java:** Usada na RMI Java.
3. **XML:** Usado em serviços Web.

#### Formatos Binários vs. Textuais
As duas primeiras estratégias (CDR do CORBA e Serialização Java) empacotam tipos de dados primitivos em **forma binária**. A terceira estratégia (XML) representa tipos de dados primitivos **textualmente**.

#### Endereçamento de Objetos Remotos
Quando um cliente invoca um método em um objeto remoto, a mensagem de invocação deve especificar **qual objeto em particular** deve executar o método. A referência de objeto remoto é o identificador desse objeto e é passado na mensagem de invocação.


