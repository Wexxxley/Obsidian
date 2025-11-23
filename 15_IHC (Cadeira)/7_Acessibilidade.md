

---
## **1. Qualidade em IHC**

A qualidade em IHC é <mark style="background: #ADCCFFA6;">avaliada pela adequação da interface e interação, garantindo que o usuário aproveite ao máximo o apoio computacional</mark> oferecido.

Os principais **Critérios de Qualidade de Uso** que enfatizam as características adequadas são:
- **Usabilidade**
- **Experiência do Usuário**
- **Acessibilidade**
- **Comunicabilidade**    

A acessibilidade é a base, pois um sistema inacessível não pode ser usado.

Durante a interação, o usuário emprega :
- **Habilidade Motora:** para agir nos dispositivos de entrada.
- **Sentidos e Percepção:** para identificar as respostas do sistema nos dispositivos de saída.
- **Capacidade Cognitiva:** para interpretar, raciocinar e planejar os próximos passos.

A acessibilidade se concentra em garantir que o sistema não crie barreiras para usuários que possuem limitações em uma ou mais dessas habilidades.

---
## **2. Deficiência Visual**

#### **A. Baixa Visão**
A redução do campo periférico dificulta a visão do todo, exigindo que a pessoa realize um grande número de varreduras visuais para perceber uma cena e, depois, integre essas visões parciais.

- **Contraste:** Prover contraste adequado entre o texto e o fundo.
- **Fontes:** Apresentar fontes grandes e ampliáveis.
- **Layout:** Evitar distância excessiva entre os componentes 
- **Ferramentas de Apoio:** Utilizam ferramentas de ampliação de imagens e ferramentas de inversão de contraste.
#### B. Cegueira
Pessoas cegas interagem principalmente pelo teclado e utilizam um software de **leitor de tela**. O usuário cego tem que memorizar uma infinidade de atalhos de teclado e tem que percorrer a tela diversas vezes para montar o modelo mental a partir do que o leitor anuncia. 

| **Problema Comum**       | **Ações de Design Recomendadas**                                                         |
| ------------------------ | ---------------------------------------------------------------------------------------- |
| **Conteúdo não-textual** | Prover equivalente textual para imagens e audiodescrição para vídeos.                    |
| **Informações por cor**  | Legendas textuais para informações não textuais (ex.: cores diferentes).                 |
| **Navegação**            | Associar rótulos e campos (label, name), cabeçalhos e células de uma tabela (header, id) |
| **Sessões Curta**        | Prever a possibilidade de prolongar as sessões na Web.                                   |
![300](../attachments/Pasted%20image%2020251123070501.png)

---
## **3. Deficiência Auditiva**

A deficiência auditiva apresenta um desafio de comunicação, pois o surdo de nascença, na maioria das vezes, não é capaz de falar. O surdo aprende a ler os lábios e se comunica por meio de linguagens de sinais (como LIBRAS).

- **Problemas Comuns:**
    - Percepção de feedback sonoro.
    - Compreender a linguagem escrita, pois muitas vezes ela é uma segunda língua.
        
- **Ações de Design para Surdez:**
    - **Conteúdo:** Adotar uma linguagem mais simples nos textos.
    - **Organização:** Apresentar as informações importantes no início do conteúdo.
    - **Visual:** Favorecer ilustrações visuais.
    - **Mídia:** Prover legendas ou transcrição textual para os conteúdos em áudio e vídeo.
    - **Assistência:** Oferecer a transcrição para a linguagem dos sinais.
	![300](../attachments/Pasted%20image%2020251123070349.png)

---
## **4. Deficiência Física**

Pessoas com deficiências físicas têm dificuldades para deslocar, controlar e coordenar movimentos, que têm alcance limitado e força reduzida.

- **Problemas Comuns:**
    - Interagir com **menus em cascata não persistentes**.
    - Clicar em comandos ou links que são pequenos, numerosos e muito próximos.
        
- **Ações de Design para Deficiência Física:**
    - Alvos Maiores 
    - Estabelecer uma **ordem de tabulação lógica** (sequência predefinida na qual o foco do teclado se move de um componente para o próximo quando o user pressiona Tab) e criar **atalhos de teclado**.
    - O usuário pode usar dispositivos adaptados, como _trackballs_ (mouse invertido), teclados de uma só mão, ou teclados virtuais .        
    ![450](../attachments/Pasted%20image%2020251123071610.png)

---
## **5. Deficiência Cognitiva e Idade**

Esta categoria engloba desde déficits de atenção e dislexia até condições como Autismo, Síndrome de Down e Demência .

- **Dificuldades:** Interpretação de estímulos visuais e auditivos, dificuldade para conversar, raciocinar, memorizar e aprender de maneira geral .
    
- **Ações de Design:**
    - Diminuir a quantidade de opções, comandos e _links_.
    - Usar linguagem simples em frases e parágrafos curtos.
    - Ilustrar textos com imagens e vídeos.
        
- **Foco em Pessoas Idosas:** O envelhecimento traz dificuldades de leitura de textos pequenos, e de controle e coordenação do _mouse_ .
    
- **Ações:** Exigem fontes grandes e ajustáveis, contraste adequado, e áreas clicáveis maiores e mais distantes umas das outras .

---
## **6. Analfabetismo e Limitações Tecnológicas**

- **Analfabetismo Funcional:** É a dificuldade de compreender textos simples.
    - **Ações:** Priorizar linguagem visual e sonora e usar frases curtas e simples .
        
- **Limitações Tecnológicas:** Conexão de baixa velocidade ou equipamentos ultrapassados.
    - **Ações:** Otimizar o desempenho dos sites e prover equivalentes de texto para imagens e vídeos (para que o sistema funcione mesmo se o gráfico não carregar).

---

## **7. Recomendações de acessibilidade**

WCAG 2 (Diretrizes de Acessibilidade para Conteúdo Web)
![550](../attachments/Pasted%20image%2020251123072120.png)

**Princípios do design universal**

**Equiparação nas possibilidades de uso:** pode ser utilizado por qualquer usuário em condições equivalentes.

**Flexibilidade de uso:** atende a uma ampla gama de indivíduos, preferências e habilidades individuais.

**Uso simples e intuitivo:** fácil de compreender, independentemente da experiência do usuário, de seus conhecimentos, aptidões linguísticas ou nível de concentração.

**Informação perceptível:** fornece de forma eficaz a informação necessária, quaisquer que sejam as condições ambientais/físicas existentes ou as capacidades sensoriais do usuário.

**Tolerância ao erro:** minimiza riscos e consequências negativas decorrentes de ações acidentais ou involuntárias.

**Mínimo esforço físico:** pode ser utilizado de forma eficiente e confortável, com um mínimo de fadiga.

**Dimensão e espaço para uso e interação:** espaço e dimensão adequados para a interação, o manuseio e a utilização, independentemente da estatura, da mobilidade ou da postura do usuário.


