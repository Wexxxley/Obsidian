

---
O principal desafio é que **diferentes computadores podem usar diferentes representações** para tipos de dados simples, como inteiros ou números de ponto flutuante (problema de heterogeneidade). O processo de transformar dados estruturados em uma sequência de bytes para transmissão é chamado de **empacotamento** (_marshalling_).

### 1. Empacotamento (Marshalling)
O empacotamento envolve a **serialização** (transformação em uma sequência de bytes) dos valores primitivos e dos tipos de dados estruturados. O processo inverso, chamado **desempacotamento** (_unmarshalling_), reconstrói a representação de dados a partir dos valores primitivos recebidos.

Estratégias de representação externa
1. **Representação Comum de Dados (CDR) do CORBA:** É uma representação externa dos tipos primitivos e estruturados que podem ser passados como argumentos e resultados na Invocação de Métodos Remotos (RMI) do CORBA. O CDR é independente da linguagem de programação.
2. **Serialização Java:** Usada na RMI Java.
3. **XML:** Usado em serviços Web.

#### Formatos Binários vs. Textuais
As duas primeiras estratégias (CDR do CORBA e Serialização Java) empacotam tipos de dados primitivos em **forma binária**. A terceira estratégia (XML) representa tipos de dados primitivos **textualmente**.

#### Endereçamento de Objetos Remotos
Esta seção também aborda a **Referência de Objeto Remoto** (Remote Object Reference). Quando um cliente invoca um método em um objeto remoto, a mensagem de invocação deve especificar **qual objeto em particular** deve executar o método. A referência de objeto remoto é o identificador desse objeto, **válido em todo o sistema distribuído**, e é passado na mensagem de invocação.

Uma referência de objeto remoto típica contém:

- **Endereço IP e número de porta:** Especifica o processo do servidor que contém o objeto remoto.
- **Tempo de criação:** Para garantir unicidade.
- **Número de um processo de servidor:** Usado internamente pelo servidor.
- **Número de um objeto remoto (ID do objeto):** Para distinguir o objeto dentro do processo.
- **Informações sobre a interface do objeto:** Por exemplo, o nome da interface, crucial para o processo receptor saber quais métodos são oferecidos pelo objeto.

Em algumas formas de referência de objeto remoto, o endereço IP e a porta podem ser usados diretamente como endereço para enviar mensagens de invocação. Contudo, para permitir que objetos remotos sejam migrados para outro computador, a referência de objeto remoto não deve ser usada como endereço. Sistemas como Pastry e Tapestry (Capítulo 10) utilizam uma forma de referência de objeto remoto **completamente independente da localização**.
