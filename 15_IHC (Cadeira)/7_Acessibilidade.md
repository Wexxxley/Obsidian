

---
## **1. Qualidade em IHC**

A qualidade em IHC é avaliada pela adequação da interface e interação, garantindo que o usuário aproveite ao máximo o apoio computacional oferecido.

Os principais **Critérios de Qualidade de Uso** que enfatizam as características adequadas são:
- **Usabilidade**
- **Experiência do Usuário**
- **Acessibilidade**
- **Comunicabilidade**    

A acessibilidade é a base, pois um sistema inacessível não pode ser usado.

---
## **2. Acessibilidade**

Durante a interação, o usuário emprega :
- **Habilidade Motora:** para agir nos dispositivos de entrada.
- **Sentidos (Visão, Audição, Tato) e Percepção:** para identificar as respostas do sistema nos dispositivos de saída.
- **Capacidade Cognitiva:** para interpretar, raciocinar e planejar os próximos passos.

A acessibilidade se concentra em garantir que o sistema não crie barreiras para usuários que possuem limitações em uma ou mais dessas habilidades.
### 1. Deficiência Visual

- **Baixa Visão:** Caracterizada por um campo visual menor do que $30^{\circ}$
- **Cegueira:** Caracterizada por um campo visual menor que $20^{\circ}$

#### **Dificuldades para Baixa Visão**

A redução do campo periférico dificulta a visão do todo, exigindo que a pessoa realize um grande número de varreduras visuais para perceber uma cena e, depois, integre essas visões parciais4.

**Ações de Design para Baixa Visão:**

- **Contraste:** Prover contraste adequado entre o texto e o fundo5.
    
- **Fontes:** Apresentar fontes grandes e ampliáveis6.
    
- **Layout:** **Aproximar rótulos, campos e comandos em um formulário**7. Pessoas com baixa visão enfrentam obstáculos devido à **distância excessiva** entre os componentes de uma zona de interação8.
    
- **Ferramentas de Apoio:** Utilizam ferramentas de ampliação de imagens e textos e de inversão de contraste9999.
    

### 2. Acessibilidade e Cegueira

Pessoas cegas interagem principalmente pelo teclado para comandar um software **leitor de tela** (ou _ledor_ de tela)10.

- **Desafio Mnemônico:** O usuário cego tem uma carga mnemônica considerável para memorizar a infinidade de atalhos de teclado e para **percorrer a tela diversas vezes** para montar o modelo mental a partir do que o leitor anuncia11. Em interfaces de toque, isso é simplificado, pois os dedos funcionam como o cursor do leitor12.
    

**Problemas Comuns (e Ações para Acessibilidade):**

|**Problema Comum**|**Ações de Design Recomendadas**|
|---|---|
|**Conteúdo não-textual**|**Prover equivalente textual para imagens** e audiodescrição para vídeos13131313.|
|**Informações por cor**|**Falta de legendas textuais** para informações não textuais (ex.: cores diferentes)14.|
|**Navegação (HTML)**|Falha em associar rótulos e campos (ex: `label`, `name`), e cabeçalhos e células de uma tabela (ex: `header`, `id`)15.|
|**Sessões Curta (Web)**|Problemas em consequência das **atualizações automáticas** e dos **tempos de validade das sessões** demasiadamente curtos16. **Ação:** Prever a possibilidade de prolongar as sessões na Web e desativar as atualizações17.|

**Tecnologias Assistivas Físicas:** Incluem teclados com letras ampliadas, teclados e telas em braile18.