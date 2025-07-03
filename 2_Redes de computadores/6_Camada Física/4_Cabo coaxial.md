
---

### **1. Estrutura do Cabo Coaxial**
O nome "coaxial" significa "com o mesmo eixo". Ele é formado por quatro camadas:

1. **Condutor Central:** Fio de cobre sólido por onde o sinal de dados principal viaja.
2. **Isolante:** Uma camada espessa de plástico que envolve o condutor. Sua espessura é fundamental para definir a **impedância** do cabo.
3. **Malha Metálica (Blindagem):** Uma malha de cobre ou alumínio trançado que envolve o dielétrico. Esta malha atua como o segundo condutor e, mais importante, como uma blindagem contra interferências.
    
4. **Capa Externa:** Uma camada de plástico protetora que envolve todo o conjunto.
   ![400](../../attachments/Pasted%20image%2020250703195127.png)
### Vantagens

A principal vantagem do cabo coaxial deriva diretamente de sua estrutura.

- **Excelente Blindagem:** A malha metálica (camada 3) cria uma "gaiola de Faraday" ao redor do condutor central. Isso o torna **extremamente resistente a interferências eletromagnéticas (EMI)** e a ruídos de radiofrequência (RFI). Essa é sua maior vantagem sobre o par trançado não blindado (UTP).
    
- **Maior Largura de Banda em Longas Distâncias:** Devido à sua blindagem superior, o coaxial consegue transportar sinais de alta frequência (como os de TV a cabo e internet banda larga) por distâncias maiores com menos perda de sinal (atenuação) em comparação ao par trançado.
    
- **Durabilidade:** Geralmente, são cabos mais robustos e resistentes fisicamente do que o par trançado.
    

### Desvantagens

Como seu slide bem aponta, essas vantagens vêm com um custo.

- **Custo Elevado:** A quantidade de material (cobre na malha, espessura do dielétrico) e o processo de fabricação o tornam mais caro que o cabo de par trançado. Os conectores (tipo F, BNC) também são mais caros e complexos.
    
- **Pouca Flexibilidade e Instalação Difícil:** São cabos mais grossos e rígidos. Isso dificulta a sua passagem por curvas apertadas, conduítes e cantos. A instalação dos conectores ("crimpar") também exige ferramentas específicas e mais habilidade.
    
- **Largura de Banda Limitada (vs. Fibra Óptica):** Embora supere o par trançado em muitos cenários, sua capacidade é vastamente inferior à da fibra óptica, que é a tecnologia dominante hoje para novas redes de alta velocidade.
    

---

### A Importância da Impedância

Este é o conceito elétrico mais importante do cabo coaxial.

- **O que é?** A **impedância** é uma medida da oposição ao fluxo de corrente alternada (AC) em uma determinada frequência. Pense nela como a "resistência" do cabo para o sinal que ele transporta. Ela é medida em **Ohms (Omega)**. A impedância de um cabo coaxial é determinada com precisão pela distância e pelo material entre o condutor central e a malha metálica.
    
- **Por que é crucial?** Para que a transferência de sinal seja máxima e sem perdas, a impedância do **cabo**, dos **conectores** e dos **equipamentos** (TV, modem, antena) **deve ser a mesma**. Isso é chamado de "casamento de impedância". Se você conectar um cabo com uma impedância a um aparelho com outra, parte do sinal é "refletida" de volta, causando perda de potência, "fantasmas" na imagem de TV analógica ou erros de dados na internet.
    

#### Padrões de Impedância

Existem dois padrões de impedância universalmente adotados para cabos coaxiais, cada um com uma aplicação específica:

1. **75 Ohms (Omega)**
    
    - **Aplicação Principal:** **Vídeo e Telecomunicações**. É o padrão usado para **TV a cabo, internet a cabo (DOCSIS), antenas de TV (digital e satélite) e outras aplicações de vídeo**.
        
    - **Motivo:** O valor de 75 Ohms representa o melhor compromisso para se obter a **menor perda de sinal (atenuação)** possível, o que é vital para enviar um sinal de TV limpo por longas distâncias.
        
2. **50 Ohms (Omega)**
    
    - **Aplicação Principal:** **Transmissão de Rádio e Dados**. É o padrão usado em **rádios comunicadores (antenas de rádio amador, transceptores), redes de computadores mais antigas (10BASE2, "Thinnet") e cabos de conexão de antenas de Wi-Fi ("pigtails")**.
        
    - **Motivo:** O valor de 50 Ohms representa o melhor compromisso para a **máxima capacidade de transmissão de potência**. É ideal quando o objetivo é enviar um sinal de rádio potente para uma antena, por exemplo.
        

Portanto, para as aplicações citadas no seu slide (TV e Internet a cabo), o cabo coaxial utilizado é sempre o de **75 Ohms**.