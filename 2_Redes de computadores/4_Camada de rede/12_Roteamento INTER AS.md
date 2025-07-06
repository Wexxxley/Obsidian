
---
### **1. BGP (Border Gateway Protocol):**

A  função do BGP é permitir que diferentes Sistemas Autônomos troquem informações de roteamento sobre os prefixos IP que controlam e os caminhos que podem usar para alcançar outros prefixos. 

Quando um Sistema Autônomo anuncia um prefixo via BGP, ele está dizendo: =="Olá, outros ASes! Eu sou o AS X, e eu sou o responsável por este bloco de endereços IP== (Ex, `203.0.113.0/24`). Se você tiver tráfego destinado a qualquer endereço IP dentro deste bloco você pode enviá-lo para mim, e eu sei como entregá-lo.

---
#### **1.2 Sessões BGP**

Usam o TCP para confiabilidade.

- **Sessão eBGP:** Usada para estabelecer sessões entre roteadores de borda em ASes vizinhos. Através delas, os ASes trocam informações de prefixos que controlam ou que podem alcançar.
- **Sessôes iBGP**: Uma vez que um roteador de borda aprende uma rota externa, ele precisa anunciar essa rota para os roteadores internos do seu AS.

![Pasted image 20250606100212](../../attachments/Pasted%20image%2020250606100212.png)
- Quando AS2 comunica um prefixo ao AS1, AS2 está prometendo que irá encaminhar todos os datagramas destinados a esse prefixo em direção ao prefixo.
- Quando um roteador aprende um novo prefixo, ele cria uma entrada para ele em sua tabela de roteamento.

---
#### **1.2 Prefixos + atributos = rota**
- **Atributo NEXT_HOP:** ==O endereço IP do próximo roteador no caminho para o prefixo de destino.==Para eBGP, é o endereço do roteador vizinho. Para iBGP, é o endereço de um roteador de borda.
- **Atributo AS_PATH:** Lista ordenada de ASes que o tráfego atravessaria para chegar ao destino. Cada vez que um prefixo é anunciado por um AS, o AS de origem adiciona seu próprio número de AS ao AS_PATH. 

---
#### **1.3 Processo de Seleção de Rota do BGP**

Um roteador pode aprender mais do que 1 rota para o mesmo prefixo. O roteador deve selecionar uma rota usando as regras de eleiminação.

**1. Atributo de Valor de Preferência Local  (LOCAL_PREF):** O `LOCAL_PREF` é um atributo BGP que é usado dentro de um AS. Ele não é propagado para outros ASes. É um valor numérico, e quanto maior o valor de `LOCAL_PREF`, maior a preferência da rota.
- **Decisão de Política:** Por exemplo nos EUA é proibido trafégo com cuba, iraque e outros países.

**2. AS-PATH caminho mais curto.** Se ainda houver múltiplas rotas candidatas, o BGP comparará o comprimento do `AS_PATH` de cada rota. A rota com o **`AS_PATH` mais curto** é preferida. A lógica é que um caminho que passa por menos AS é, em teoria, mais direto.

**3. Roteador do NEXT-HOP mais próximo.** O `NEXT_HOP` é o endereço IP do roteador que é o próximo salto no caminho para o prefixo de destino. Se ainda houver múltiplos caminhos, o roteador precisará decidir qual gateway usar para sair do seu AS. O roteador BGP consultará sua própria tabela de roteamento interna e escolhe a rota alcançada com o menor custo.

**4. Critérios Adicionais.**: Se, após todos os critérios acima, ainda houver empate, o BGP recorrerá a critérios adicionais, que podem variar ligeiramente.

---
#### **1.4 Inter AS vs Intra AS**
- Inter-AS: a administração quer ter controle sobre como seu tráfego é roteado e sobre quem roteia através da sua rede. Políticas podem ser dominantes em relação ao desempenho.
- Intra-AS: administração única, então não são necessárias políticas de decisão. Preocupação com desempenho.

